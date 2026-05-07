# **Supported Dropdown Embedded Commands**

A dropdown label may include any of the following tokens.  
They can appear **anywhere**, in **any order**, and the system will automatically detect and schedule them.

## **Quick Cheat‑Sheet**

You can embed commands directly inside dropdown labels.  
Everything after `|` is hidden from the visible label.

**Supported tokens:**

- `CC-x-y` → Control Change  
- `PC-x` → Program Change  
- `NRPN-x-y` → NRPN parameter  
- `NOTE-ON-x-y` / `NOTE-OFF-x-y` → Play/stop notes  
- `RAW-xx_xx_xx` → Raw MIDI bytes  
- `WAIT-x` → Delay next command(s)  
- `PRE-ANY ...` → Commands before main action  
- `POST-ANY ...` → Commands after main action  
- `BTN-x` → Quick‑access button

**Line continuation:**  
Prefix a line with `..` to join it with the previous one.

Example:

```
Preset 1
.. hellow
.. | NOTE-ON-41-28
Preset 2
..world
..| NOTE-ON-42-28
```

Becomes:

```
Preset 1 hellow | NOTE-ON-41-28
Preset 2 world | NOTE-ON-42-28
```

---

## MIDI Control Commands

| Token | Meaning |
|-------|---------|
| `CC-x-y` | Send Control Change **x** with value **y** |
| `PC-x` | Send Program Change **x** |
| `NRPN-x-y` | Send NRPN parameter **x** with value **y** |

---

## Note Commands

| Token | Meaning |
|-------|---------|
| `NOTE-ON-x-y` | Play note **x** with velocity **y** |
| `NOTE-OFF-x-y` | Stop note **x** with velocity **y** |

---

## Raw MIDI Message

| Token | Meaning |
|-------|---------|
| `RAW-x` | Send a raw MIDI message, where **x** is a sequence of hex bytes separated by underscores |

**Examples**

```
RAW-90_3C_64
```

- 90 → Note On, Channel 1  
- 3C → Note 60 (Middle C)  
- 64 → Velocity 100  

```
RAW-F0_7E_7F_09_01_F7
```

Sends a SysEx message.

---

## Timing Commands

| Token | Meaning |
|-------|---------|
| `WAIT-x` | Delay the next command(s) by **x ms** |

**Notes**

- WAIT **does not block** the UI or server thread.  
- Delays accumulate:

```
WAIT-100 WAIT-200  → total delay = 300 ms
```

- Commands scheduled for the same timestamp execute **in label order**.

---

## PRE-ANY and POST-ANY

Dropdown entries beginning with `PRE-ANY` or `POST-ANY` define additional commands that run **before** or **after** the main dropdown command.

Use cases include:

- Resetting LED indicators  
- Preparing controller state  
- Cleanup actions after the main command  

These tokens never appear in the visible dropdown label.

---

## Quick-Access Button Token

| Token | Meaning |
|-------|---------|
| `BTN-x` | Adds a quick-access button with sort order **x** |

**Details**

- Clicking the button instantly selects that dropdown item.  
- If ordering doesn’t matter, use `BTN-0` for all.

---

# **Examples**

## Program Change with Bank Select

```
Item 0, default send zero for whatever is defined in user control
Item 1, that sends program change | CC-0-5 CC-32-0 PC-3
```

**Item 1 sends:**

- `CC 0 → 5` (Bank Select MSB)  
- `CC 32 → 0` (Bank Select LSB)  
- `PC 3` (Program Change)

## Control surface indication on preset change.

```
PRE-ANY NOTE-ON-41-0 NOTE-ON-42-0  
Preset 1 | NOTE-ON-41-28
Preset 2 | NOTE-ON-42-28
```
---

## Notes + Timing Example

```
NOTE-ON-60-100 WAIT-500 NOTE-OFF-60-50
```

Sequence:

1. Play note 60 at velocity 100  
2. Wait 500 ms  
3. Stop note 60 at velocity 50  

