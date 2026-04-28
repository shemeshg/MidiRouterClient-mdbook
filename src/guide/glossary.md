# Glossary

Quick reference for MIDI and application-specific terminology.

---

## MIDI Concepts

### CC (Control Change)
A MIDI message that conveys continuous control data (e.g., volume, expression). Each CC has a number (0–127) and a value (0–127). Often called "continuous controllers."

### Note On / Note Off
MIDI messages that represent playing a note. Note On includes note number (pitch) and velocity. Note Off indicates when the note is released.

### Program Change (PC)
A MIDI message that selects a program or preset on a connected device. Values 0–127 represent different programs.

### NRPN (Non-Registered Parameter Number)
A higher-resolution MIDI message for controlling parameters beyond standard CCs. Uses four bytes: NRPN MSB, NRPN LSB, Data MSB, Data LSB. Allows 16,384+ unique parameter addresses.

### RPN (Registered Parameter Number)
Similar to NRPN but standardized. Examples include Pitch Bend Sensitivity (RPN 0) and fine/coarse tuning.

### Pitch Bend
A continuous MIDI message for pitch shifting. Range: -8192 to +8191 (center = 0).

### Aftertouch
MIDI messages sent after a key is pressed. Two types:
- **Channel Aftertouch** — Single value for entire keyboard
- **Polyphonic Aftertouch** — Individual value per note

### MIDI Clock (Timing Clock)
Timing signal sent 24 times per quarter note, used to synchronize tempo across devices.

### SPP (Song Position Pointer)
A MIDI message indicating playback position in a sequence. Sent 2 times per quarter note.

### 14-bit CC Resolution
Combining two standard 7-bit CCs (MSB and LSB) to achieve finer control. Allows 0–16,383 resolution instead of 0–127.

### Sysex (System Exclusive)
Manufacturer-specific MIDI messages for device control. Format varies by manufacturer.

---

## Application Concepts

### Preset
A named collection of:
- Routing rules (Routes)
- Input port settings
- User controls (sliders, dropdowns)

Presets can be activated by mouse click, MIDI event, or program change.

### Route
A processing pipeline for MIDI data. Contains one or more **Chains**, each with a sequence of **Filters**. Routes define how input MIDI is transformed and where it's sent.

### Chain
A linear sequence of filters within a route. MIDI flows through each filter in order.

### Filter
A single transformation or routing rule. Examples:
- Route to MIDI destination
- Transform CC values
- Send to remote server
- Schedule for delayed playback

### EasyConfig
Simplified UI for creating basic routes without writing filter definitions. Generates a full Route behind the scenes. Great for learning.

### User Control
On-screen interactive element (slider, dropdown) that sends MIDI commands when manipulated. Associated with a specific preset.

### Virtual MIDI Port
Software-based MIDI port created by the application (no physical hardware). Allows internal routing between software. Not supported on Windows 11 with MIDI 2.0.

### Monitoring
Real-time inspection of incoming MIDI messages. Translates complex formats (NRPN, 14-bit CC) into human-readable labels.

### Port Settings
Configuration for how a physical/virtual input port handles MIDI:
- Which message types to ignore
- How to handle MIDI clock
- 14-bit CC translation
- Others

### Configuration File
JSON file storing the entire application state:
- All presets
- All routes
- User control definitions
- Connection bookmarks

Located in the server folder, accessible from the **Login** tab.

### Headless Mode
Running the application without a GUI. Useful for server deployments or scripting. Activated via CLI flags.

### Connection Bookmark
Saved connection profile for connecting to remote servers. Stores IP address and port.

---

## Common Abbreviations

| Term | Full Name |
|------|-----------|
| CC | Control Change |
| PC | Program Change |
| NRPN | Non-Registered Parameter Number |
| RPN | Registered Parameter Number |
| SPP | Song Position Pointer |
| MSB | Most Significant Byte |
| LSB | Least Significant Byte |
| GUI | Graphical User Interface |
| CLI | Command-Line Interface |

