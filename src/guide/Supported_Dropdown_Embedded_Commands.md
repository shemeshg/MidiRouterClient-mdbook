# **Supported Dropdown Embedded Commands**

A dropdown label may include any of the following tokens.  
They can appear **anywhere in the label**, in **any order**, and the system will automatically detect and schedule them.

## **MIDI Control Commands**

| Token | Meaning |
|-------|---------|
| `CC-x-y` | Send Control Change *x* with value *y* |
| `PC-x` | Send Program Change *x* |
| `NRPN-x-y` | Send NRPN parameter *x* with value *y* |

## **Note Commands**

| Token | Meaning |
|-------|---------|
| `NOTE-ON-x-y` | Play note *x* with velocity *y* |
| `NOTE-OFF-x-y` | Stop note *x* with velocity *y* |

Notes are passed internally as a `QStringList`, so even a single note is handled consistently with multi‑note APIs.

## **Timing Commands**

| Token | Meaning |
|-------|---------|
| `WAIT-x` | Delay the next command(s) by *x* milliseconds |

WAIT does **not** block the Server/UI thread.  
Instead, commands are scheduled preserving order.

Multiple WAITs accumulate:

```
WAIT-100 WAIT-200  → total delay = 300 ms
```

Commands scheduled at the same delay fire in the order they appear.

## PRE‑ANY and POST‑ANY 

Dropdown entries that begin with the tokens PRE-ANY or POST-ANY define additional commands that run before or after the main dropdown command.

This mechanism is useful for tasks such as resetting multiple LED indicators and lighting the correct one for the selected entry, or performing any other setup/cleanup actions around the main command.

---

## **Example**

Selecting Program **3** in Program Bank **5**:

```
PRE‑ANY this becomes like remarks never appear on dropdown
PRE‑ANY NOTE-OFF-80-0 NOTE-OFF-81-0 
Item 0,  default send zero for whatever is defined in user control
Item 1, that sends program change | CC-0-5  CC-32-0  PC-3
Item 2, light on 80 | NOTE-ON-80-0
```

Commands after `|` are processed internally but hidden from the dropdown label to keep it readable.

Item 1 sends:

- `CC 0 → 5` (Bank Select MSB)  
- `CC 32 → 0` (Bank Select LSB)  
- `PC 3` (Program Change)

---

## **Example with Notes and Timing**

```
NOTE-ON-60-100 WAIT-500 NOTE-OFF-60-50
```

This will:

1. Play note 60 at velocity 100  
2. Wait 500 ms  
3. Stop note 60 at velocity 50  



