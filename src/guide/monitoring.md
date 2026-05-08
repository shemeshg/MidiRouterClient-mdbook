# Monitoring MIDI Messages

Debug and inspect incoming MIDI data in real-time.

## Overview

The Monitoring view shows all MIDI messages arriving at the selected input port, translating complex MIDI data into a readable format for quick, intuitive troubleshooting. You can also open the monitor in a separate window to keep it visible while working elsewhere in the app.

Monitoring can additionally be enabled by inserting a `monitor` filter anywhere in the chain. Since it behaves like any other filter, it lets you inspect or debug the flow without altering the chain’s logic. Output can be sent either to the server console or to the client where the input originates, giving you flexibility in how and where you observe activity.

---

## How to Use

1. Navigate to the **In Ports** tab
2. Select your input device from the port list
3. Click **Monitoring**

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

- Input device is recognized  
- MIDI data arrives without errors  
- Message types match expectations  
- Value ranges are correct  
- No timing issues.
- Debig custom `chain filter`s.
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
