---
name: opentrons-machine
description: Generate commands and full protocols for Opentrons OT-2 liquid handling robots, including labware loading, tip management, pipetting, protocol code generation, CSV-driven loops, and camera image capture.
---

# Opentrons Machine

Use for **automated liquid handling and full protocol generation on the Opentrons OT-2 robot**.

## Capabilities

- Full protocol code generation via `Protocol.to_python_code()` - produces valid runnable OT-2 Python
- Pipetting workflows: `aspirate`, `dispense`, `transfer` (with auto-chunking for large volumes)
- Tip management: `pick_up_tip`, `drop_tip`
- Deck and labware setup: `load_labware`, `load_instrument`
- Flow control: `flow_rate`, `air_gap`, `blow_out`, `touch_tip`, `move_to`
- Protocol utilities: `delay`, `comment`, `home`
- CSV-driven loops: `read_csv_file` + `loop` for data-driven protocols
- Custom labware support: AMDM mass balance vials (30 mL, 50 mL) loaded inline
- All gen2 pipette types: p10, p20, p300, p1000 (single and multi-channel)
- **External camera image capture**: `camera_capture` - triggers the external camera mounted above the deck to capture and save a still image of the wellplate

## Use This Machine When

- The user references an Opentrons OT-2 robot
- The task involves generating a complete OT-2 protocol or individual liquid handling commands
- The user mentions Opentrons labware (tip racks, well plates, reservoirs, NEST, Corning, mass balance vials)
- The workflow requires data-driven dispensing from a CSV file
- The workflow requires capturing a camera image of the wellplate after dispensing steps

## Before Command Generation

- Refer to: [opentrons-machine](references/opentrons-machine.md)
- Run `puda machine commands opentrons` to understand available commands
- Follow all command types, params, sequencing rules, and labware constraints in `references/opentrons-machine.md`

## Workflow

1. Parse user intent and confirm the task requires the Opentrons machine.
2. Load the Opentrons machine reference and CLI help.
3. Confirm required physical setup details with the user, especially deck slots, pipette type, mount, labware names, source wells, destination wells, and transfer volumes.
4. Generate PUDA protocol commands with `machine_id: "opentrons"`.
5. Validate command sequencing against the machine reference before returning or running a protocol.
6. Do not run robot movement unless the user explicitly approves execution.

## Critical Sequencing Rules

- `opentrons` protocols must always end with no tip attached to any pipette.
- `opentrons` deck slot (`location`) for every `load_labware` command must be explicitly confirmed by the user - **never assume a slot**.
- `opentrons` `capture_image` must be its own standalone protocol - never combined with pipetting commands in the same protocol.
