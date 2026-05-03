# **Supported Dropdown Embedded Commands**

A dropdown label may include any of the following tokens.  
They can appear **anywhere**, in **any order**, and the system will automatically detect and schedule them.

---

## MIDI Control Commands

| Token | Meaning |
|-------|---------|
| `CC‑x‑y` | Send Control Change **x** with value **y** |
| `PC‑x` | Send Program Change **x** |
| `NRPN‑x‑y` | Send NRPN parameter **x** with value **y** |

---

## Note Commands

| Token | Meaning |
|-------|---------|
| `NOTE‑ON‑x‑y` | Play note **x** with velocity **y** |
| `NOTE‑OFF‑x‑y` | Stop note **x** with velocity **y** |

---

## Raw MIDI Message

| Token | Meaning |
|-------|---------|
| `RAW‑x` | Send a raw MIDI message, where **x** is a sequence of hex bytes separated by underscores |

**Examples**

```
RAW-90_3C_64
```

- 90 → Note On, Channel 1  
- 3C → Note 60 (Middle C)  
- 64 → Velocity 100  

```
RAW‑F0_7E_7F_09_01_F7
```

Sends a SysEx message.

---

## ⏱️ Timing Commands

| Token | Meaning |
|-------|---------|
| `WAIT‑x` | Delay the next command(s) by **x ms** |

**Notes**

- WAIT **does not block** the UI or server thread.  
- Delays accumulate:

```
WAIT-100 WAIT-200  → total delay = 300 ms
```

- Commands scheduled for the same timestamp execute **in label order**.

---

## 🔁 PRE‑ANY and POST‑ANY

Dropdown entries beginning with **PRE‑ANY** or **POST‑ANY** define additional commands that run **before** or **after** the main dropdown command.

Use cases include:

- Resetting LED indicators  
- Preparing controller state  
- Cleanup actions after the main command  

These tokens never appear in the visible dropdown label.

---

## ⚡ Quick‑Access Button Token

| Token | Meaning |
|-------|---------|
| `BTN‑x` | Adds a quick‑access button with sort order **x** |

**Details**

- Clicking the button instantly selects that dropdown item.  
- higher `x` = earlier in the button row.  
- If ordering doesn’t matter, use `BTN‑0`.

---

# **Examples**

## Program Change with Bank Select

```
PRE‑ANY NOTE-OFF-80-0 NOTE-OFF-81-0
Item 0, default send zero for whatever is defined in user control
Item 1, that sends program change | CC-0-5 CC-32-0 PC-3
Item 2, light on 80 | NOTE-ON-80-0
```

Commands after `|` are internal and hidden from the label.

**Item 1 sends:**

- `CC 0 → 5` (Bank Select MSB)  
- `CC 32 → 0` (Bank Select LSB)  
- `PC 3` (Program Change)

---

## Notes + Timing Example

```
NOTE-ON-60-100 WAIT-500 NOTE-OFF-60-50
```

Sequence:

1. Play note 60 at velocity 100  
2. Wait 500 ms  
3. Stop note 60 at velocity 50  

