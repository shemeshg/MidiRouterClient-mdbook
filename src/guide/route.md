# Route

A **Route** is a container for multiple chains, enabling modular and sequential processing of MIDI data.

### Learning to Create Routes

If you're trying to understand how routes are built, the easiest way is to start with an `EasyConfig`. Once you've created one, inspect how it's automatically translated into a full route. This reverse-engineering method offers a hands-on, intuitive way to grasp the structure and logic of route creation—without needing to dive into low-level details right away.

---

## Chains

A **chain** defines a linear path composed of a sequence of **filters**. Each filter performs a specific transformation or analysis on the MIDI stream, allowing for flexible and customizable data manipulation as it flows through the chain.

---

# Filter Types

### `TO_MIDI_DESTINATION`
Routes MIDI events to a specific local MIDI destination.

### `TO_CONSOLE`
Logs MIDI events to the console (either server or client). This filter is also used for inter-server communication, such as sending logged MIDI messages to a client or triggering preset changes via MIDI.

### `TO_NETWORK`
Sends all MIDI events to a remote destination.

### `SCHEDULE_TO`
Holds MIDI events and schedules them for future delivery based on `deferredType` and `deferredTo` parameters. Requires MIDI clock events to function properly.

### `FILTER_AND_TRANSFORM`
Allows both filtering and transforming MIDI event data. Transformation notation includes:

- `[[fromStart, fromEnd, toStart, toEnd]]` — Maps a range from `fromStart` to `fromEnd` onto `toStart` to `toEnd`.
- `[[fromStart, fromEnd, toStart]]` — Short form where `toEnd = toStart + (fromEnd - fromStart)`.
- `[[value1, value2]]` — Maps `value1` to `value2`.
- `[[value]]` — Equivalent to `[[value, value]]`, a single value mapping.


### `SWITCH_DATA1_DATA2`
Swap **data1** and **data2**, or swap **NRPN control** and **NRPN data** when using **NRPN**.
This can be useful, for example, when routing a **Note On** key value to **CC** data.

# 📚 Reference

### Filter Type 0: `TO_MIDI_DESTINATION`

**Parameters:**
- `filterType`: `0`
- `midiInputName`: Name of the MIDI input port

---

### Filter Type 1: `TO_CONSOLE`

**Parameters:**
- `filterType`: `1`
- `logTo`: Logging destination
  - `0` (CLIENT): Client console
  - `1` (SERVER): Server console
- `userdata`: Optional user-defined JSON data

---

### Filter Type 2: `TO_NETWORK`

**Parameters:**
- `filterType`: `2`
- `midiInputName`: MIDI input port name
- `serverName`: Target server name
- `serverPort`: Target server port


---

### Filter Type 3: `SCHEDULE_TO`

**Parameters:**
- `filterType`: `3`
- `deferredType`: Scheduling mode
  - `0`: IN_SPP (relative to Song Position Pointer)
  - `1`: IN_BAR (relative to current bar)
  - `2`: AT_SPP (specific SPP)
  - `3`: AT_BAR (specific bar)
  - `4`: QUANTIZE_SPP (nearest SPP)
  - `5`: QUANTIZE_BAR (nearest bar)
- `deferredTo`: Number of units to defer

---

### Filter Type 4: `FILTER_AND_TRANSFORM`

**Parameters:**
- `conditionAction`: Event deletion logic
  - `0`: DO_NOT_DELETE
  - `1`: DELETE_IF_NOT_MET_CONDITION
  - `2`: DELETE_IF_MET_CONDITION
- `filterChannel`: MIDI channel filter
- `filterData1`: Data1 byte filter/transform
- `filterData2`: Data2 byte filter/transform
- `filterEvents`: MIDI event types to filter (e.g., `[8]` for Note On)
- `filterType`: `4`
- `name`: Filter name

---

### Filter Type 5: `SWITCH_DATA1_DATA2`