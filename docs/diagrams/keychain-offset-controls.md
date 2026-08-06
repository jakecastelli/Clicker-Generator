# Keychain two-axis positioning

## Current flow

```mermaid
flowchart LR
  P["Position angle"] --> E["Find body edge anchor"]
  S["Slide offset"] --> T["Move along edge tangent"]
  E --> A["Keychain anchor"]
  T --> A
```

At the top of the design, the edge tangent runs left to right, so the current offset cannot move the keychain toward or away from the body.

## Target flow

```mermaid
flowchart LR
  P["Position angle"] --> E["Find body edge anchor and outward direction"]
  S["Slide offset"] --> T["Move along edge tangent"]
  D["In / out offset"] --> R["Move along outward direction"]
  E --> A["Combined keychain anchor"]
  T --> A
  R --> A
  A --> G["Generate loop and bridge"]
```

The final anchor is computed as:

`edge anchor + tangent * slide offset + outward direction * in/out offset`

- Slide offset keeps the existing left/right fine-tuning.
- In / out offset adds movement toward or away from the clicker body.
- Both offsets remain relative to the selected position angle.
