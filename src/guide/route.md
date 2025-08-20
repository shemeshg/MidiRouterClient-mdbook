# Route

A Route is a container for multiple chains, enabling modular and sequential processing of MIDI data.

### Learning to Create Routes

If you're looking to understand how routes are constructed, the easiest way is to start by creating an `EasyConfig`. Once it's defined, inspect how the system translates it into a full route. This reverse-engineering approach offers a practical and intuitive way to learn the structure and logic behind route creation—without diving into the complexity upfront.

## Chains

A `chain` defines a linear path composed of a series of `filters`. Each filter performs a specific transformation or analysis on the MIDI stream, allowing for flexible and customizable data manipulation as it traverses the chain.


