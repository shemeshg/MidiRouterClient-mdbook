# Configuration

The configuration includes essential information such as:

- **Connected Inputs and Outputs**  
  A list of currently active MIDI ports.

- **Presets**  
  Settings for both connected and disconnected ports, including:
  - Routing definitions
  - User control mappings (e.g., sliders, dropdowns)

- **Dropdowns**  

    Dropdowns allow users to select values using friendly labels, but the label itself may also contain embedded MIDI commands.

    It is generated from the **User Control definition**, and may optionally include one or more embedded MIDI instructions.

    When an embedded command is present, the **User Control’s normal action is not executed**.  
    Instead, the embedded MIDI commands take priority and are sent immediately.

    ### Supported Embedded Commands

    A dropdown label may include:

    - `CC-x-y` — Send Control Change *x* with value *y*
    - `PC-x` — Send Program Change *x*
    - `NRPN-x-y` — Send NRPN parameter *x* with value *y*

    These tokens may appear **anywhere in the label** and in **any order**.  
    The application automatically detects them and triggers the corresponding MIDI messages.

    ### Example

    Select Program **3** in Program Bank **5**:

    ```
    Item default send zero for what ever defined in user control
    Item that send program change CC-0-5  CC-32-0  PC-3
    ```

    2nd item sends:

    - `CC 0 → 5` (Bank Select MSB)
    - `CC 32 → 0` (Bank Select LSB)
    - `PC 3` (Program Change)


- **Virtual Ports**  
  Definitions for virtual MIDI ports used for internal routing.  
  ⚠️ *Note: Virtual ports are currently not supported on Windows.*



## Persist configuration

Configuration is stored in a `json` file. Since the schema may change with version upgrades, it's recommended to back up your configuration regularly.

To simplifying the process of persisting changes, In the `login` tab, you can manage automatically load on application start and save on close.

Clicking the `link` at `login` tab redirects to the server folder where the JSON configuration is stored. You can copy this file for backup.

The `⋮` button provides `about` information and options to download or upload and apply the current configuration.

---

# Screenshots

Settings 

<img src="Screenshot 2025-08-20 at 6.29.42.png" style="width:60%; height:auto;" />

Login tab

<img src="Screenshot 2025-08-20 at 6.42.51.png" style="width:60%; height:auto;" />

