# Port Settings

Configure how your MIDI input ports handle incoming messages.

## Overview

Port settings control message filtering, clock handling, and value translation at the input level. Changes apply only to the **active preset** and **selected input port**.

> **Note:** Settings are preset-specific. Different presets can have different configurations for the same port.

---

## Key Settings

### Ignore Message Types

Select which types of MIDI messages to discard at the input:

- **Sencee** — Device connected indication
- **MIDI Clock** — Timing synchronization signals
- **Sysex** — Manufacturer-specific commands


**Tip:** Enable "Ignore MIDI Clock" if your device floods the log with timing data and you're not using tempo sync.

---

## MIDI Clock Settings

Configure how **MIDI Clock** and **Song Position Pointer (SPP)** messages are processed.

### Options

- **Convert SPP to time signature** — Translate song position into bar/beat notation
- **Propagate clock** - Propagate to other inputs

**Use case:** When syncing multiple devices based on selected clock

---

## 14-bit CC Translation

Convert **dual CC messages** (MSB/LSB) into higher-resolution formats.

### When to Use

- Converting **14-bit CC to Pitch Wheel** for finer pitch control
- Mapping **14-bit CCs to NRPN values** for parameter precision
- Increasing resolution from 0–127 to 0–16,383 (though internaly represented as float 0..127)


---

## Screenshots

**Figure 1: Port Settings Configuration**  
Toggle message types, configure MIDI clock, and enable 14-bit translation.

<img src="Screenshot 2025-08-20 at 6.58.34.png" style="width:60%; height:auto;" />

---

## Common Workflows

### Workflow 1: Filter Out Timing Noise
Many devices send constant MIDI Clock signals, cluttering the interface.

1. Select your input port
2. Enable **"Ignore MIDI Clock"**
3. Clock messages are now discarded
4. ✅ Cleaner monitoring and debugging

### Workflow 2: Enable High-Resolution Control
Route a 14-bit CC fader to pitch wheel for smoother control.

1. Select input device
2. Enable **"14-bit CC Translation"**
3. Choose source CCs (e.g., CC 7, this will also use CC 39 automaticlly)
4. Choose target format (e.g., Pitch Wheel)
5. ✅ Fader now controls pitch smoothly

---

## See Also

- [Monitoring](monitoring.md) — Inspect incoming messages in real-time
- [In Ports Overview](inport.md)
- [Glossary: MIDI Clock, SPP, 14-bit CC](glossary.md)
