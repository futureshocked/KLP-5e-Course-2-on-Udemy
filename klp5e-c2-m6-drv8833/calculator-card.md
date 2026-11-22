# Calculator card: what the calculator decided (L6.2)

The numbers from Lecture 6.2, worked in KiCad 10.0.7's Calculator Tools, and the net class value each one
leads to. Lecture 6.4 types these values into the three classes.

All widths come from "Power, current and isolation", "Track Width": IPC 2221, a 10 °C rise, 1 oz/ft²
copper, read from the "External Layer Tracks" panel. Both layers of a two-layer board are external. The
calculator takes 1 oz as 34.4 µm.

## Track widths

| Nets | Current | Calculator | Class gets | Why |
|---|---|---|---|---|
| `VM`, `GND` (the supply and its return) | 3 A | 1.39 mm | `Power` 1.50 mm | Rounded up from 1.39 mm. A class carries one width, sized for its worst member. |
| `AOUT1`, `AOUT2`, `BOUT1`, `BOUT2` (the bridge outputs) | 1.5 A | 0.53 mm | `Power` 1.50 mm | Covered by `Power`: more copper than they need, which is fine. |
| `AISEN`, `BISEN` (the sense nets) | 1.5 A | 0.53 mm | `Sense` 0.60 mm | `Default` is too thin (below). `Power` is too wide: 1.50 mm is longer than a 1206 pad (1.125 mm). |
| `AIN1`, `AIN2`, `BIN1`, `BIN2`, `nSLEEP`, `nFAULT` and the rest (everything the controller touches) | a few mA | 0.25 mm carries 0.86 A | `Default` 0.25 mm | Plenty for these nets, but too thin for the sense nets. |

A class width is what KiCad routes at, not a limit it enforces. A net routed too thin for its current
raises no error.

## Clearance

"Electrical Spacing", "IPC 2221" tab, row "0 .. 15 V" (`VM` is at most 10.8 V): B2 (bare external
track) 0.10 mm, A6 (track at a component lead) 0.13 mm.

Voltage does not set this board's clearance. Manufacturing does: 0.30 mm on `Power`, 0.20 mm on `Sense`
and `Default`.

## One power via

"Via Size": finished hole 0.4 mm, pad 0.8 mm, plating 0.025 mm, via length 1.6 mm, 3 A, 10 °C rise.

| Reading | Value |
|---|---|
| Estimated ampacity | 2.31 A (under the 3 A the net carries) |
| The same current as a track | 0.97 mm, cross-section 0.0334 mm² |

One via has about two thirds of the copper in the 1.50 mm track feeding it. Wherever a power net changes
layer, it goes through two vias.

## These numbers belong to this board

If you copy this project for another board, its classes come with it, so check them against that
board's currents.
