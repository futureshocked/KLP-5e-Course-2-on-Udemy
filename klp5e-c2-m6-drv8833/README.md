# klp5e-c2-m6-drv8833 stages

One folder per step of the capstone of Modules 6, 8, 9 and 11: a two-motor driver board built round the DRV8833,
using the symbol and footprint you authored in Modules 1 and 2. The module draws the sheet, sets
the board up, places the driver stage first, routes the board and writes the rule that covers the chip's breakout,
pours the ground, labels the silkscreen and finishes it with the title block and logos. Each stage
is the project as it stood at the end of a lecture or bonus video and the start of the next one.

**Every stage is a complete KiCad project.** Open the `.kicad_pro` in a stage folder and it loads
on its own: the schematic, the board, the project's symbol and footprint library tables,
`Libraries/` (the DRV8833 symbol and footprint) and `datasheets/`. From `05-board-setup` on, the
stage also holds the `.kicad_dru` custom rules. Each stage also holds `tools/checknet.py`, the
netlist checker, and `tools/checkplacement.py`, the placement checker. Copy a stage folder out of
the repository before you work in it, and do not open two stages at once.

| Stage | State | Produced by |
|---|---|---|
| `00-start` | An empty A4 sheet with the title block, an empty board, the `Default` net class only, the DRV8833 library and datasheet, and the two checkers | bonus B6.1 |
| `01-classes-and-stage` | The `Power` and `Sense` net classes and their four patterns; the eight-part driver stage placed on the sheet, unannotated and unwired | lecture 6.4 |
| `02-sheet-placed` | Every part placed and annotated, with values and footprints filled in; still no wire | bonus B6.2 |
| `03-wired` | The sheet wired and labelled; ERC reports two `power_pin_not_driven` errors | lecture 6.5 |
| `04-netlist-clean` | Two `PWR_FLAG`s added; ERC clean; checknet's three checks pass | lecture 6.6 |
| `05-board-setup` | The fabricator's limits and mask clearance imported, default severities, two copper layers, the two-rule `.kicad_dru`; the board is still empty | lecture 6.7 |
| `06-outline` | Predefined track and via sizes, silkscreen default 0.15 mm, the 20 footprints on the board, the outline drawn | bonus B6.3 |
| `07-stage-placed` | The eight driver-stage parts placed; the other twelve still off the board | lecture 6.8 |
| `08-all-placed` | Every part at its table position, the driver stage locked; the board agrees with the sheet | bonus B6.4 |
| `09-bridge-a` | `VM_IN`, `VM`, `AOUT1`, `AOUT2` and `AISEN` routed on `F.Cu`. The start of A6.1 | lecture 6.9 |
| `10-bridge-b` | `J3` re-pinned and bridge B routed: `BOUT1`, `BOUT2` and `BISEN`. The worked solution to A6.1 | bonus B6.5 |
| `11-logic-routed` | The logic nets routed; only `GND` is left unconnected | bonus B6.6 |
| `12-breakout-area` | The rule area `U1_breakout` drawn round the chip, with a deliberate what-if: two narrow pieces on `AOUT1` and `BOUT1` that the DRC flags while the rule still follows the courtyard | lecture 6.10 |
| `13-rule-on-area` | The breakout rule aimed at the rule area; the DRC is clear | lecture 6.11 |
| `14-ground-poured` | The `GND` pour on both layers, with ties to the back for the ground pads in pockets of front copper. One tie via is still at the default size | lecture 6.12 |
| `15-labelled` | The designators and the connector legends on the silkscreen | lecture 6.13 |
| `16-finished` | The title block and the KiCad and Tech Explorations logos; the DRC reports no violation and parity is clean. The finished board, and the start of Modules 8 and 9 | bonus B6.7 |
| `16u1-fields-added` | The four sourcing field templates in the project; `U1`'s supplier fields corrected; `J1` to `J3`, `R2` and `R3` filled | lecture 8.2 |
| `16u2-fields-filled` | `MPN`, `Manufacturer` and `Supplier` filled on all 13 lines of the bill | bonus B8.1 |
| `16u3-without-sense` | The design variant `without-sense`, with its overrides on `R2` and `R3` | lecture 8.3 |
| `16u4-bills-exported` | The bill's export file set to `BOM/bom_${VARIANT}.csv`; `BOM/` holds one bill for each build | lecture 8.5 |
| `16u5-assembly-bill` | The assembler's template columns and BOM names saved in the project; `BOM/` also holds the bill shaped to the template | lecture 8.6 |
| `17-dfm-checked` | The same board after the DRC with the fab's numbers and the HQ DFM plugin; neither needed a fix | lecture 9.2 |
| `18-finish-enig` | The surface finish set to ENIG in Board Setup; nothing else changed | lecture 9.3 |
| `19-plotted` | The plot settings saved; `Gerber/` holds the nine Gerbers, the drill file and its map, the job file, the position file and `klp5e-c2-m6-drv8833-fab.zip`, the archive sent to the factory | lecture 9.4 |
| `20-fab-checked` | The same files after the three checks on the plotted files; nothing needed a fix. This is the board that was ordered, and the start of Module 11 | lecture 9.5 |
| `21-control-bus` | The four control lines drawn as the bus `CTRL{AIN1 AIN2 BIN1 BIN2}`; the board's control nets are now `/CTRL.AIN1` to `/CTRL.BIN2` | lecture 11.2 |
| `22-logic-table` | The DRV8833's H-bridge logic table on the back silkscreen | lecture 11.3 |
| `23-qr-code` | A QR code made with the footprint wizard and saved as `te_qr_code` in `peters_custom_Library`, on the back silkscreen | lecture 11.4 |
| `24-teardrops` | Teardrops on the board's pads and vias; pours refilled | lecture 11.5 |

Stage `16-finished` adds a second project library, `Logo` (`Libraries/Logo.pretty`), holding the Tech
Explorations logo footprints. Its row is in the stage's `fp-lib-table`.

Stages `16u1` to `16u5` are Module 8: the sourcing fields, the `without-sense` build and the bills.
They branch off `16-finished`, and Module 9 does not continue from them. `17-dfm-checked` follows
`16-finished`, not `16u5-assembly-bill`, so the stages from `17` on have no sourcing fields and no
variants.

Stages `17` to `20` are the board as it was checked and ordered in Module 9. Stages `21` to `24`
are the recipes of Module 11: touches for the board's next revision, so they hold no plotted files
and nothing in them was ordered.

## Checking the netlist (lecture 6.6)

From a stage folder, from `03-wired` on:

```bash
kicad-cli sch export netlist -o net.net klp5e-c2-m6-drv8833.kicad_sch
python3 tools/checknet.py net.net --nets
python3 tools/checknet.py net.net --u1-pins
python3 tools/checknet.py net.net --classes
```

On `04-netlist-clean` and later, all three pass.

## Checking the placement (bonus B6.4)

From a stage folder, from `08-all-placed` on:

```bash
python3 tools/checkplacement.py --outline --fit --overlap --proximity
```

On `07-stage-placed` it fails, because twelve parts are still off the board.

## Activity A6.1

[`A6.1-activity/`](A6.1-activity/) has everything for the activity in its own README: where you
start, the task, the settings, the acceptance list and what to do if you get stuck. The folder also
holds a record sheet (`record-sheet.md`) and the lecture's slide deck (`slides.html`). Start from
`09-bridge-a`. The worked solution is bonus B6.5, and its stage is `10-bridge-b`.

## Reference pages

Three pages in this folder carry the reasoning that the lectures summarise:

1. [`calculator-card.md`](calculator-card.md): the Calculator Tools results from lecture 6.2 and
   the net class value each one leads to.
2. [`HOW_THE_BOARD_WORKS.md`](HOW_THE_BOARD_WORKS.md): the whole board on one sheet, as lecture 6.3
   shows it, and the reasoning behind each value the datasheet leaves to you.
3. [`WHY_WITHOUT_SENSE.md`](WHY_WITHOUT_SENSE.md): why the `without-sense` build of Module 8 can
   replace the sense resistors with `0R`, with the datasheet's lines and page numbers.
