# Input Ports

The **In Ports** tab is where you configure how MIDI inputs are processed and routed.

## Overview

Only ports that are currently connected will be shown. The In Ports tab has three main functions:

1. **[Port Settings](port_settings.md)** — Filter message types, configure MIDI clock, enable 14-bit translation
2. **[Monitoring](monitoring.md)** — Inspect incoming MIDI messages in real-time
3. **[Routing](#routing-options)** — Create or configure routes for incoming data

> **Note:** All settings are preset-specific. Different presets can have different configurations for the same port.

---

## Quick Links

- 📊 **[Port Settings](port_settings.md)** — Configure message filtering and value translation
- 🔍 **[Monitoring](monitoring.md)** — Real-time MIDI inspection and debugging

---

## Routing Options

You can set up routing in two ways:

### **EasyConfig** (Recommended for Beginners)
A simple, guided tool that helps you create routing setups without needing to dive into technical details. Perfect for learning.

**Best for:**
- First-time setups
- Simple A-to-B routing
- Quick testing

### **Routes** (Advanced)
Full control over routing configurations. Build custom filter chains, transformations, and complex workflows.

**Best for:**
- Custom transformations
- Multi-stage processing
- Scheduling and advanced features

**How they work together:** EasyConfig automatically generates a full Route behind the scenes. After creating an EasyConfig, inspect the generated Route to understand advanced concepts.

---

## Getting Started

1. Select an input port from the list
2. (Optional) Adjust [Port Settings](port_settings.md) for filtering/translation
3. (Optional) Use [Monitoring](monitoring.md) to verify data arrival
4. Create a route using **EasyConfig** or **Routes**
5. Test with [Monitoring](monitoring.md)

---

## See Also

- [Getting Started](getting_started.md)
- [EasyConfig](easyConfig.md)
- [Routes](route.md)
- [Glossary](glossary.md)
