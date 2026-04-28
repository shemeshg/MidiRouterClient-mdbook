# Getting Started

Welcome to MIDI Router Client! This guide walks you through the core concepts and gets you routing MIDI in under 10 minutes.

## The Big Picture

MIDI Router Client works around three key concepts:

1. **Presets** — Collections of routing rules and controls grouped together
2. **Routes** — Instructions for how MIDI data flows from input to output
3. **User Controls** — On-screen sliders and dropdowns that send MIDI commands

**Typical workflow:** Install → Create Preset → Add Route (EasyConfig) → Add User Controls → Test & Deploy

---

## Step 1: Install MIDI Router Client

Choose your platform:

- **Windows**: [Use scoop](installation.md#windows)
- **macOS**: [Use Homebrew](installation.md#macos)  
- **Linux**: [Download prebuilt packages](installation.md#linux)

---

## Step 2: Create Your First Preset

A preset is where you store everything: routes, controls, and port settings.

1. Open **MIDI Router Client**
2. Navigate to the **Presets** tab
3. Click **New Preset** and name it (e.g., "My First Setup")
4. (Optional) Set activation mode to **"select"** for MIDI-triggered preset switching

✅ **Done!** Your preset is ready to use. Now it's time to route MIDI.

---

## Step 3: Create Your First Route

For beginners, use **EasyConfig** instead of manually building routes—it's much simpler.

1. Navigate to the **In Ports** tab
2. Select your connected MIDI input device
3. Click **EasyConfig** (not Routes)
4. Follow the guided setup:
   - Choose your input device
   - Choose your output destination
   - (Optional) Select which MIDI messages to filter or transform (e.g., CC, Note On)

**Want to learn the advanced way?** Once you've created an EasyConfig, inspect the generated **Route** to see how it works. This reverse-engineering method is the fastest way to master routes.

---

## Step 4: Add User Controls (Optional)

User controls are interactive sliders and dropdowns on-screen.

1. Navigate to **User Controls**
2. Click **New Control**
3. Choose a type (Slider, Dropdown, etc.)
4. Configure which MIDI message it sends (CC, Program Change, NRPN)
5. Set the range and labels

Now you can trigger MIDI commands with a mouse click or touch.

---

## Step 5: Test & Debug

Use **Monitoring** to verify MIDI data:

1. Go to **In Ports** tab
2. Select your input device
3. Click **Monitoring**
4. Send MIDI to your input — you should see messages logged in real-time

**Troubleshooting tips:**
- MIDI clock messages appearing as junk? Enable "Ignore MIDI Clock" in Port Settings
- 14-bit CC values showing as two separate messages? Use "14-bit CC Translation" in port settings
- Not sure what that NRPN is? Monitoring translates it to human-readable format

---

## Next Steps

Now that you have a basic setup working:

- **Learn Routes deeply**: Read [Route documentation](route.md) for filter types and advanced configurations
- **Master Presets**: Check out [Preset activation modes](preset.md) for MIDI-triggered switching
- **Advanced Routing**: Explore [Configuration options](configuration.md) for remote servers and clock manipulation
- **Reference**: Consult the [complete filter reference](reference.md) for all available transformations

---

## Common Scenarios

### Scenario 1: Route a Keyboard to a Synth
1. Create a preset named "Keyboard → Synth"
2. Use EasyConfig to map your keyboard input to the synth output
3. EasyConfig will route all events default
4. ✅ Done! Press keys on your keyboard to control the synth

### Scenario 2: Create a Custom Mixer with Sliders
1. Create a preset
2. Add a route forwarding CC messages
3. In User Controls, add 8 sliders (CC 7, 10, 11, etc.)
4. Label them (Volume, Pan, Reverb, etc.)
5. ✅ Now control multiple parameters with on-screen sliders

### Scenario 3: Switch Setups with MIDI
1. Create multiple presets (e.g., "Rock Setup", "Jazz Setup")
2. In each preset, set activation mode to "select"
3. Assign a Program Change number to trigger each preset
4. ✅ Send Program Change from your controller to instantly switch presets

---

## Need Help?

- **Confused by a term?** Check the [Glossary](glossary.md)
- **Looking for a specific feature?** Browse the [Complete Reference](reference.md)
- **Want to understand the technical details?** Read [Configuration](configuration.md)
- **Advanced users?** See [Advanced: CLI Reference](cli_reference.md) for automation
