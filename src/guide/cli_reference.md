# Advanced: CLI Reference

Run MIDI Router Client from the command line for scripting, automation, and headless deployments.

## Availability

- **macOS** and **Linux**: CLI included with application
- **Windows**: Install CLI tool via `scoop install -g midi-router-client-cli` 

---

## Basic Syntax

```bash
./midi-router-client [options]
```

---

## Options Reference

### Information

| Option | Effect |
|--------|--------|
| `-h, --help` | Display command-line help message |
| `--help-all` | Display help including generic Qt options |

### Headless Mode

```bash
./midi-router-client --headless
```

Runs the application without a GUI. Useful for server deployments or background automation.

**Additional options for headless:**
- `--config-file <path>` — Full path to configuration file
- `--server-port <port>` — Server port number

### Apply Preset

```bash
./midi-router-client --apply \
  --address <address> \
  --preset-name <preset>
```

Applies a preset on the local machine or remote server. Returns exit code `0` on success.

**Parameters:**
- `--address <address>` — Remote address in format `ip:port` (e.g., `127.0.0.1:2222`)
- `--preset-name <preset>` — Preset name or regex pattern; use `""` to list all presets

---

## Examples

### Example 1: List All Available Presets

```bash
./midi-router-client --apply --address 127.0.0.1:2222 --preset-name ""
```

Outputs all preset names available on the specified server.

---

### Example 2: Apply a Specific Preset Locally

```bash
./midi-router-client --apply --preset-name "neutron"
```

Activates the "neutron" preset on the local machine.

---

### Example 3: Apply a Preset on Remote Server

```bash
./midi-router-client --apply --address 192.168.1.100:2222 --preset-name "studio"
```

Activates the "studio" preset on a remote server at `192.168.1.100:2222`.

---

### Example 4: Start in Headless Mode

```bash
./midi-router-client --headless \
  --config-file /path/to/config.json \
  --server-port 2222
```

Starts the server without a GUI, loads the configuration, and listens on port 2222.

---

## Exit Codes

| Code | Meaning |
|------|---------|
| `0` | Success |
| `1` | Error or failure |

The exit code is particularly useful for scripting and automation — check it to verify if an `--apply` operation succeeded.

---

## Use Cases

### Use Case 1: Automated Preset Switching

Trigger preset changes from cron jobs or external scripts:

```bash
# Every hour at 30 minutes past, switch to "practice" preset
30 * * * * /path/to/midi-router-client --apply --preset-name "practice"
```

---

### Use Case 2: Remote Server Management

Deploy MIDI Router Client on a headless server and control it remotely:

```bash
# On server:
./midi-router-client --headless --config-file config.json --server-port 2222

# From client machine:
./midi-router-client --apply --address server.local:2222 --preset-name "main"
```

---

### Use Case 3: Script Validation

Verify preset application succeeded before proceeding:

```bash
#!/bin/bash
./midi-router-client --apply --preset-name "gig"
if [ $? -eq 0 ]; then
  echo "✅ Preset applied successfully"
else
  echo "❌ Preset application failed"
  exit 1
fi
```

---

## See Also

- [Configuration](configuration.md)
- [Getting Started](getting_started.md)
