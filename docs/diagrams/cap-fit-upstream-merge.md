# Cap fit control during the upstream merge

## Current canonical flow

```mermaid
flowchart LR
  U["User sees 0.00 mm"] --> S["Switch socket +/- stepper"]
  S --> T["Hidden base clearance: 0.40 mm"]
  T --> W["Grow cap well footprint"]
  W --> F["Cap-to-base fit changes"]
  U -. "actual issue is unclear" .-> R["Cap rubs base"]
```

The canonical control still changes the cap-to-base clearance, but the visible value is an offset from 0.40 mm and the switch-oriented label obscures what is being adjusted.

## Target flow

```mermaid
flowchart LR
  U["User"] --> C["Cap fit tolerance slider\n0.20 to 0.80 mm"]
  C --> T["Actual clearance value"]
  T --> W["Grow cap well footprint"]
  W --> F["Cap clears base wall"]

  U --> B["Switch body clearance"]
  B --> H["Grow base socket cutout"]

  U --> M["Switch stem tolerance"]
  M --> X["Scale cap stem socket"]
```

The merge keeps the newer canonical features while presenting each physical fit as a separate control:

- Cap fit tolerance adjusts the cap-to-base gap and displays the actual millimetre value.
- Switch body clearance adjusts the MX housing cutout in the base.
- Switch stem tolerance adjusts how the cap stem grips the MX switch.
