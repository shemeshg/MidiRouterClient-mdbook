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

WAIT does **not** block the UI thread.  
Instead, commands are scheduled preserving order.

Multiple WAITs accumulate:

```
WAIT-100 WAIT-200  → total delay = 300 ms
```

Commands scheduled at the same delay fire in the order they appear.

---

## **Example**

Selecting Program **3** in Program Bank **5**:

```
Item default send zero for whatever is defined in user control
Item that sends program change CC-0-5  CC-32-0  PC-3
```

This sends:

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



