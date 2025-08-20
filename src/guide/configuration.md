# Configuration

The configuration includes essential information such as:

- **Connected Inputs and Outputs**  
  A list of currently active MIDI ports.

- **Presets**  
  Settings for both connected and disconnected ports, including:
  - Routing definitions
  - User control mappings (e.g., sliders, dropdowns)

- **Dropdowns**  
  A mapping between user-friendly preset names and their corresponding `Program Change` IDs.

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

