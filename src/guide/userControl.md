# User Controls

Each preset can include interactive controls such as sliders, optionally paired with dropdown menus.

User controls can be programmed to trigger MIDI messages to any port when the `Midi Router Client` receives program changes

Only the controls associated with the currently selected preset are displayed.

These controls send MIDI events to a predefined local port. The following MIDI event types are supported:

- **Control Change (CC)**
- **Program Change**
- **NRPN (Non-Registered Parameter Number)**

The `is64Mode` flag interprets the value `64` as the center or zero point, commonly used for bipolar ranges.

Dropdowns can also be used to store and select predefined preset names.

---

## Screenshots

**Figure 1: User Controls Panel**  
The main controls view showing available sliders and dropdowns for the active preset.

<img src="Screenshot 2025-08-20 at 10.15.17.png" style="width:60%; height:auto;" />

**Figure 2: Individual Control Configuration**  
Detailed settings for a single control (e.g., CC range mapping, event type).

<img src="Screenshot 2025-08-20 at 10.04.11.png" style="width:60%; height:auto;" />

---

## See Also

- [Getting Started](getting_started.md) — Quick onboarding guide
- [Presets](preset.md) — Organize controls in presets
- [Supported Dropdown Commands](Supported_Dropdown_Embedded_Commands.md) — Advanced dropdown features
- [Glossary](glossary.md) — MIDI terminology reference

