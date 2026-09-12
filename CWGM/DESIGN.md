# CWGM dual-sink clamshell

Living design brief for a 3D-printed OpenMANET enclosure around the CWGM radio stack. Copy this file for the next enclosure, keep the section order, and replace the content. When the model is printable, lift Overview, Philosophy, Parts, and Assembly into `README.md` using the same shape as OpenNot5 / OpenChubNET.

| Field | Value |
|-------|--------|
| Status | Design in progress — envelope approved, CAD not started |
| Date | 2026-09-12 |
| Working name | CWGM (Fusion document name; public name TBD) |
| CAD | Autodesk Fusion, document `Full v2` / `CWGM` |
| Repo home | `enclosures/CWGM/` |

## Decisions

Record each locked choice here so a later session does not re-litigate it.

| Decision | Choice | Why |
|----------|--------|-----|
| Battery | Waveshare UPS HAT D + 2× 21700 | Already in the Fusion library; pogo-pin Pi HAT, 56 × 85 mm |
| Packing | In-line: radio first, battery bay at one end | Dual heatsinks block stacking the HAT under the board |
| Shell | Two-piece clamshell | User request; opens radio and battery together |
| Split plane | Face split — midplane of the PCB, parallel to the heatsinks | Each half owns one full heatsink window; no seam across fins |
| Heatsink treatment | Recess / window like Robdoe | Aluminum sinks sit in the shell, fins exposed |
| Width target | ~80 mm (Robdoe main-body width) | Keeps the handheld proportion; 528 sinks are ~61 × 58 mm |

## Still open

- Public enclosure name
- Exact Wakefield SKU on the live stack (528-45AB ~11.4 mm vs 528-24AB ~6.1 mm)
- Which short end is battery vs I/O, and which connectors need panel cutouts
- Screw standard (assume M3 through the four stack holes + perimeter screws unless Fusion shows otherwise)
- Print material (other OpenMANET prints prefer ABS/ASA)
- Whether fins sit flush or proud of the shell
- Fusion MCP must be reconnected before modeling

## Intent

Wrap the CWGM board so it can be carried like the Robdoe / OpenNot5 radio, with three changes from that reference:

1. Smaller heatsinks, one on each face of the board
2. Battery inside the same shell (not a slide-on pack)
3. The board’s mounting holes are how the electronics are held

## Reference: Robdoe / openMANET case

Local STLs (not in this repo): `~/Desktop/Offgrid/OpenMANET/3D/openMANET case/`

| Part | Bounding box (mm) | Role |
|------|-------------------|------|
| Main body | 80 × 45 × 140 | Shell; large one-sided heatsink |
| Front panel | 80 × 18 × 94.5 | I/O end |
| Back panel | 80 × 8.5 × 133 | Opposite end |
| Battery pack (slide-on) | 80 × 45 × 122.5 | Waveshare 3S, external |
| Slide lock | ~8 × 14 × 21 | Retains the pack |

Robdoe language to keep: rectangular handheld, heatsink sitting in a recess with fins to air, connectors on the short ends.

Robdoe language to drop: single giant 559-class sink on one face only; three-piece body + end caps; external slide-on battery.

Screenshots of the printed reference: `~/Downloads/Robdoe/`.

## Hardware in Fusion

| Item | Notes |
|------|--------|
| CWGM | Custom board, Pi-like I/O (USB, Ethernet). Dual heatsink sandwich. Thumbnail shows a generic grey box as placeholder only. |
| Heatsinks | Wakefield 528-series, both faces. 528-45AB: 60.96 × 57.91 × 11.43 mm, 11 fins, 4× Ø3.18 mm. 528-24AB: same footprint, shorter (~6.1 mm). Confirm which is in the open assembly. |
| Stack thickness | A Fusion measurement of 25.495 mm matches two 11.4 mm sinks + PCB + pads. Treat as the radio thickness until the live model is measured. |
| Mounting | Four corner holes through sinks and board. `Full v2` (saved 2026-09-12) is a 4-hole rectangular frame/gasket on that pattern. |
| UPS HAT D | 56 × 85 mm Pi HAT, 2× 21700 in parallel, 5 V Type-C charge, pogo pins to a Pi. Cannot use pogo pins through a bottom heatsink — power the radio by cable/USB from the HAT in the adjacent bay. |
| Other library parts (not committed to this case) | CM4 / CM4-IO-BASE, Pi 4, WM1302, Weipu SP13, Amphenol RF, Guide Orion C 0635CS, UPS Module 3S |

Do not modify the CWGM board model. Enclosure is a new design that references it.

## Architecture

Two deep trays meet on the PCB midplane.

```
  [ I/O end ][ radio: sink / board / sink ][ UPS HAT D + 21700s ][ charge end ]
                    ^ face-split seam around the perimeter
                    ^ each tray has one heatsink window
```

- Each tray: one rectangular window + recess. The aluminum sink drops in; fins face out; a rim hides the sink base.
- The four stack holes clamp board + both sinks between the halves (long screws into inserts in one tray). Extra perimeter screws keep the battery bay closed.
- UPS HAT D lives in the in-line bay. 21700s come out when the clamshell opens — no separate hatch.
- Connectors and the HAT Type-C sit on the two short ends.

Rejected alternatives:

- Edge (left/right) split — seam across the fins
- Stacking the HAT under the radio — blocked by the bottom sink; pogo pins would not reach
- Beside layout — wider than Robdoe
- Robdoe 3-piece + hatch — user chose clamshell

## Envelope (approved 2026-09-12)

| Dimension | Target | Basis |
|-----------|--------|-------|
| Width | ~80 mm | Robdoe; sink 61 mm + rim |
| Thickness | stack (~25.5 mm) + walls | Fins flush or slightly proud |
| Length | ~160–180 mm | Radio + HAT 85 mm + 21700s + end walls. One body replaces Robdoe’s 140 mm radio + 122 mm pack. |

Numbers are planning targets. Replace with measured Fusion bounding boxes before sketching.

## Parts (draft)

Required:

- CWGM board (as in the Fusion session)
- 2× Wakefield 528-series heatsinks (SKU TBD from the live stack)
- Waveshare [UPS HAT D](https://www.waveshare.com/ups-hat-d.htm)
- 2× 21700 Li-ion cells
- Printed clamshell, 2 pieces
- Fasteners for the four stack holes + perimeter (M3 assumed)
- Power lead from HAT USB / 5 V out to the radio (pogo pins unused)

Optional / I/O TBD: antennas, bulkheads, charge-port gland, power switch.

## Assembly (intended)

1. Seat one heatsink in the window of tray A.
2. Place CWGM on that sink, holes aligned; add the four-hole frame if the stack uses it.
3. Seat the second heatsink in tray B (or on the board) so both windows are filled when closed.
4. Fit UPS HAT D and cells in the battery bay; cable 5 V to the radio.
5. Close the clamshell; screw through the stack holes into inserts; add perimeter screws.
6. Fit end-face connectors last.

## CAD / file map

| Path | What |
|------|------|
| Fusion `CWGM` | Radio + dual sinks (+ placeholder box) |
| Fusion `Full v2` | 4-hole gasket/frame; most recently saved |
| Fusion `wakefield-528-45AB-part` / `528-24AB-part` | Sink models from 2026-09-10 |
| Fusion `UPS-HAT_D` | Battery board |
| `~/Desktop/Offgrid/OpenMANET/3D/openMANET case/*.stl` | Robdoe reference prints |
| `~/Desktop/Offgrid/OpenMANET/3D/Original 3D models/UPS-HAT-D 3D Drawing.zip` | Official HAT STEP |
| This file | Source of truth until `README.md` exists |

## Next CAD steps

1. Reconnect Fusion MCP and measure the open assembly (stack bbox, hole pattern, I/O keep-outs, which 528 is used).
2. New Fusion design. Do not edit CWGM.
3. Sketch one tray from the measured envelope; window and recess from the sink bbox plus clearance.
4. Mirror / derive the second tray.
5. Battery-bay pocket from the HAT STEP.
6. End-face ports once I/O is listed.
7. Export STLs here; then write `README.md` from the Overview / Parts / Assembly sections above.

## Reuse

For another enclosure, copy this folder, delete the CWGM-specific tables, and fill the same headings: Decisions, Still open, Intent, Reference, Hardware, Architecture, Envelope, Parts, Assembly, CAD map. Keep decisions in the table so a later agent can continue without the chat.
