# MIDI Configuration Overview

This document describes how configuration, presets, routing, and user‑control dropdowns work within the application. It also explains how configuration is stored and how users can manage it through the interface.


## Connected Inputs and Outputs

The configuration includes a list of all currently active MIDI ports.  
These ports may be physical or virtual (where supported).



## Presets

Presets store settings for both connected and disconnected ports. A preset may include:

- Routing definitions  
- User control mappings (sliders, dropdowns, etc.)

Presets allow you to quickly restore a complete setup without manually reconfiguring each port.


## Dropdowns

Dropdowns allow users to select values using friendly labels.  
A label may also contain **embedded MIDI commands**, which override the default user‑control behavior.

### How Dropdowns Work

- Dropdown items are generated from the **User Control definition**.  
- A label may optionally include one or more embedded MIDI instructions.  
- When embedded commands are detected, the **normal User Control action is skipped**.  
  Instead, the embedded MIDI messages are sent immediately.

### Supported Embedded Commands

A dropdown label may include any of the following tokens:

- `CC-x-y` — Send Control Change *x* with value *y*
- `PC-x` — Send Program Change *x*
- `NRPN-x-y` — Send NRPN parameter *x* with value *y*

These tokens may appear **anywhere in the label** and in **any order**.  
The application automatically detects them and sends the corresponding MIDI messages.

### Example

Selecting Program **3** in Program Bank **5**:

```
Item default send zero for whatever is defined in user control
Item that sends program change CC-0-5  CC-32-0  PC-3
```

The second item sends:

- `CC 0 → 5` (Bank Select MSB)  
- `CC 32 → 0` (Bank Select LSB)  
- `PC 3` (Program Change)

## Virtual Ports

Virtual MIDI ports can be defined for internal routing.  
⚠️ *Note: Virtual ports are currently not supported on Windows.*


## Persisting Configuration

Configuration is stored in a `json` file.  
Because the schema may change between versions, it is recommended to back up your configuration regularly.

### Automatic Load/Save

The **Login** tab allows you to load the configuration when the application starts, 
and save it when the application closes or when changes are applied (with throttling).

### Accessing the Configuration File

Clicking the **link** in the Login tab opens the server folder where the JSON configuration is stored.  
You can copy this file for backup.

### Additional Options

The `⋮` menu provides:

- **About** information  
- Options to **download**, **upload**, and **apply** the current configuration  
- Accessibility (font size)
- UI preferences, monitor in external dialog.

## cli options available for `linux` and `macos` only

Since the application does not automatically re‑apply its configuration when MIDI devices disconnect or reconnect, it can be useful to trigger a re‑apply through the CLI — both for local and remote servers. 
A successful apply operation returns exit code 0.

```
Usage: ./midi-router-client [options]

Options:
  -h, --help  Displays help on commandline options.
  --help-all  Displays help, including generic Qt options.
  --headless  Run in headless mode on the specified port by the gui.
  --apply     Apply a preset (local or remote).
               --address <address>      Remote address (ip:port).
               --preset-name <preset>   Preset name (regex) to apply, use "" to
              list presets

 example:
  ./midi-router-client  --apply --address 127.0.0.1:2222 --preset-name "neutron"
```



---

## Screenshots

### Settings  
<img src="Screenshot 2025-08-20 at 6.29.42.png" style="width:60%; height:auto;" />

### Login Tab  
<img src="Screenshot 2025-08-20 at 6.42.51.png" style="width:60%; height:auto;" />

