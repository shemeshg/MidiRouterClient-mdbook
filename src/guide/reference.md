# Reference

## Event Types

The valuee used at the `json` mapped to `midi event id`

```json
[
  { "value": 0, "text": "[] - -" },
  { "value": 1, "text": "[8, 9] - Note on/off" },
  { "value": 2, "text": "[9] - Note off" },
  { "value": 3, "text": "[8] - Note on" },
  { "value": 4, "text": "[10] - Key Aftertouch" },
  { "value": 5, "text": "[11] - Control Change" },
  { "value": 7, "text": "[100] - NRPN" },
  { "value": 8, "text": "[12] - Program Change" },
  { "value": 9, "text": "[13] - Channel Aftertouch" },
  { "value": 10, "text": "[14] - Pitch Bend" }
]
```

### Preset configuration example 
Users aren't expected to manually edit or create `json` files—this example is provided solely to help you understand the configuration structure. 

As the configuration grows, it may become increasingly difficult to grasp its overall purpose. It's recommended to maintain a separate README file outside the app to document and explain your configuration.

__Routing a Control Change (CC) event to NRPN, using channel 6 for both, and mapping a value range from 0–127 to 0–255.__


```json
{
  "midiRoutePresets": [
    {
      "midiRouteInputs": [
        {
          "midiInputName": "0_Launch Control XL",
          "easyConfig": {
            "easyConfigRoutes": [
              {
                "fromCcOrNrpnEnd": 127,
                "fromCcOrNrpnStart": 0,
                "fromChannel": 6,
                "fromData1": -1,
                "fromSelectedMidiEventTypeId": 5,
                "splitRangeId": -1,
                "toCcOrNrpnEnd": 255,
                "toCcOrNrpnStart": 0,
                "toChannel": 6,
                "toData1": 8,
                "toDestinationName": "localhost:12345/0_Scarlett 2i4 USB",
                "toSelectedMidiEventTypeId": 7,
                "transpose": 0,
                "uuid": "d3bc0cb8-0de6-43ec-94c5-91b4a6ed7c6d"
              }
            ],
            "keyboardSplits": [],
            "zoneNames": []
          }
        }
      ]
    }
  ]
}
```

## List of Midi CC commands

Some of these commands may be reserved, although certain devices might not reserve them at all and instead use them for different functions. The following list represents a common convention, but individual devices are not strictly required to adhere to it.


```
bankselectcoarse: 0,
modulationwheelcoarse: 1,
breathcontrollercoarse: 2,
footcontrollercoarse: 4,
portamentotimecoarse: 5,
dataentrycoarse: 6,
volumecoarse: 7,
balancecoarse: 8,
pancoarse: 10,
expressioncoarse: 11,
effectcontrol1coarse: 12,
effectcontrol2coarse: 13,
generalpurposeslider1: 16,
generalpurposeslider2: 17,
generalpurposeslider3: 18,
generalpurposeslider4: 19,
bankselectfine: 32,
modulationwheelfine: 33,
breathcontrollerfine: 34,
footcontrollerfine: 36,
portamentotimefine: 37,
dataentryfine: 38,
volumefine: 39,
balancefine: 40,
panfine: 42,
expressionfine: 43,
effectcontrol1fine: 44,
effectcontrol2fine: 45,
holdpedal: 64,
portamento: 65,
sustenutopedal: 66,
softpedal: 67,
legatopedal: 68,
hold2pedal: 69,
soundvariation: 70,
resonance: 71,
soundreleasetime: 72,
soundattacktime: 73,
brightness: 74,
soundcontrol6: 75,
soundcontrol7: 76,
soundcontrol8: 77,
soundcontrol9: 78,
soundcontrol10: 79,
generalpurposebutton1: 80,
generalpurposebutton2: 81,
generalpurposebutton3: 82,
generalpurposebutton4: 83,
reverblevel: 91,
tremololevel: 92,
choruslevel: 93,
celestelevel: 94,
phaserlevel: 95,
databuttonincrement: 96,
databuttondecrement: 97,
nonregisteredparametercoarse: 98,
nonregisteredparameterfine: 99,
registeredparametercoarse: 100,
registeredparameterfine: 101
```

