# Monitoring MIDI Messages

Debug and inspect incoming MIDI data in real-time.

## Overview

The Monitoring view displays all MIDI messages arriving at your selected input port. It translates complex MIDI formats into human-readable output, making troubleshooting fast and intuitive.

---

## How to Use

1. Navigate to the **In Ports** tab
2. Select your input device from the port list
3. Click **Monitoring**
4. Send MIDI to your input — messages appear instantly
5. Use the log to verify:
   - Data is arriving
   - Expected message types appear
   - Values are in the expected range

---

## What You'll See

### Simple Messages

```
Note On    | Channel 1 | Note: C4 (60) | Velocity: 100
Note Off   | Channel 2 | Note: E4 (64) | Velocity: 0
CC         | Channel 1 | CC 7 (Volume) | Value: 95
Pitch Bend | Channel 1 | Value: +2048
```

### Complex Messages (Auto-Translated)

Instead of raw bytes, the monitor shows friendly names:

**14-bit CC →** `CC 7 Hi (MSB) + CC 39 Lo (LSB) = 12,288`

**NRPN →** `NRPN #4 "Filter Cutoff" = 5,432`

**SysEx →** `SysEx (manufacturer: Roland) [F0 41 10 42 12 40 00 10 ... F7]`

---

## Common Patterns

### Pattern 1: MIDI Clock Flooding

**Problem:** Monitor is flooded with clock messages  
**Cause:** Device sends 24 clock messages per quarter note  
**Solution:** Enable [Port Settings](port_settings.md) → "Ignore MIDI Clock"

```
MIDI Clock  (every 40ms)
MIDI Clock  (every 40ms)
MIDI Clock  (every 40ms)
```

### Pattern 2: 14-bit Values Split Across Two Messages

**Problem:** Fader sends two separate CC messages instead of one smooth value  
**Cause:** Device uses MSB/LSB 14-bit encoding  
**Solution:** Enable [Port Settings](port_settings.md) → "14-bit CC Translation"

```
CC 7 (Volume MSB) = 100
CC 39 (Volume LSB) = 50
```

After translation:
```
CC 7 Volume = 12,850 (out of 16,383)
```

### Pattern 3: Nothing Appearing?

**Debugging steps:**
1. **Verify physical connection** — Is the cable plugged in?
2. **Check device is active** — Is the MIDI input showing in the port list?
3. **Check routing** — Is this the correct input port?
4. **Send test data** — Press a key/turn a knob on your device
5. **Try a different device** — Confirm the port itself works

---

## Using Monitor for Setup Verification

Before building complex routes, use monitoring to confirm:

✅ Input device is recognized  
✅ MIDI data arrives without errors  
✅ Message types match expectations  
✅ Value ranges are correct  
✅ No timing issues

---

## Performance Tips

- Monitoring can be CPU-intensive with high-frequency data (e.g., MIDI Clock)
- Disable MIDI Clock in Port Settings to reduce logging overhead
- Close monitoring when not actively debugging

---

## See Also

- [Port Settings](port_settings.md) — Configure message filtering and translation
- [In Ports Overview](inport.md)
- [Glossary: MIDI Message Types](glossary.md)
