# Route

**TL;DR:** Routes are sequences of **chains**, each containing **filters** that transform MIDI data. Start with **EasyConfig** to learn by example, then inspect the generated Route.

A **Route** is a container for multiple chains, enabling modular and sequential processing of MIDI data.

## Learning to Create Routes

If you're trying to understand how routes are built, the easiest way is to start with an `EasyConfig`. Once you've created one, inspect how it's automatically translated into a full route. This reverse-engineering method offers a hands-on, intuitive way to grasp the structure and logic of route creation—without needing to dive into low-level details right away.

---

## Common Scenarios

### Scenario 1: Route Keyboard to Synthesizer

**Goal:** Send all MIDI from keyboard to synth output

**Setup:**
1. Use EasyConfig
2. Input: Keyboard
3. Output: Synthesizer (MIDI destination)

**Result:** Every key press and control movement on keyboard goes to synth.

---

### Scenario 2: Transform CC to Pitch Wheel

**Goal:** Convert a slider (CC 11) into pitch wheel data for smoother control

**Setup:**

Backend already aware for 14bitCc if enabled at the input port

1. Create a filter with type `FILTER_AND_TRANSFORM`
2. Set `filterData1` to accept CC 11 values.
3. Set `eventype` from CC to pitch.
4. Route to synth output

**Result:** Slider now controls pitch smoothly instead of in 127 discrete steps.

---

### Scenario 3: Schedule Notes for Quantized Playback

**Goal:** Record MIDI notes and play them back on the next bar boundary

**Setup:**
1. Create a route with `SCHEDULE_TO` filter
2. Set `deferredType` to `QUANTIZE_BAR` (align to nearest bar)
3. Ensure MIDI clock is being received
4. Route output to instrument

**Result:** Notes are held and released on quantized grid positions.

---

## Chains

A **chain** defines a linear path composed of a sequence of **filters**. Each filter performs a specific transformation or analysis on the MIDI stream. Filters execute in order, so output of one filter becomes input to the next.

---

## Filter Types

### `TO_MIDI_DESTINATION`
Routes MIDI events to a specific local MIDI destination.

**Use case:** Send keyboard MIDI to a synthesizer, sampler, or drum machine.

---

### `TO_CONSOLE`
Logs MIDI events to the console (either server or client). This filter is also used for inter-server communication, such as sending logged MIDI messages to a client or triggering preset changes via MIDI.

**Use case:** Debug routing issues, send MIDI to remote servers.

---

### `TO_NETWORK`
Sends all MIDI events to a remote destination over the network.

**Use case:** Route MIDI to another computer running MIDI Router Client Server.

---

### `SCHEDULE_TO`
Holds MIDI events and schedules them for future delivery based on `deferredType` and `deferredTo` parameters. Requires MIDI clock events to function properly.

**Use case:** Quantize notes to beat grid, delay messages by bar count.

---

### `FILTER_AND_TRANSFORM`
Allows both filtering and transforming MIDI event data. Advanced value mapping for precise control.

**Use case:** Convert CC ranges, filter specific channels, map Note On to CC, etc.

**Transformation notation:**
- `[[fromStart, fromEnd, toStart, toEnd]]` — Maps a range from `fromStart` to `fromEnd` onto `toStart` to `toEnd`
- `[[fromStart, fromEnd, toStart]]` — Short form where `toEnd = toStart + (fromEnd - fromStart)`
- `[[value1, value2]]` — Maps `value1` to `value2`
- `[[value]]` — Equivalent to `[[value, value]]`, a single value mapping

---

### `SWITCH_DATA1_DATA2`
Swap **data1** and **data2**, or swap **NRPN control** and **NRPN data** when using **NRPN**.

**Use case:** Route Note On key values to CC data, swap NRPN parameters.

---

## 📚 Reference: Detailed Parameters

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