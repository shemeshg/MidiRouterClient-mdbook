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
{
    "channel": 1,
    "command": 8,
    "commandStr": "noteoff",
    "data": [
        128,
        73,
        0
    ],
    "data1": 73,
    "data2": 0,
    "deltatime": 0.18201804100000002,
    "msgtype": 0,
    "nrpnControl": -1,
    "nrpnData": -1,
    "portName": "0_Launch Control XL",
    "portNumber": 1,
    "userdata": "{\n    \"action\": \"monitor\"\n}\n"
}
```

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
