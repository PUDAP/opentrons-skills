---
name: opentrons-workflow
description: Generate and understand Opentrons OT-2 workflows, including example well-plate patterns that use explicit aspirate and dispense operations. Use when selecting, setting up, or generating Opentrons workflow protocols.
---

# Opentrons Workflow

Use this skill for Opentrons OT-2 workflow guidance and protocol generation.

## Workflows

### Example P Shape (`example`)

Use for **creating a P-shaped liquid pattern on an Opentrons OT-2 destination plate**.

Capabilities:
- Generates an OT-2 Python protocol that dispenses into a fixed set of wells shaped like the letter `P`
- Uses explicit `pipette.aspirate(...)` and `pipette.dispense(...)` calls for each destination well
- Supports configurable source labware, destination labware, tip rack, pipette, deck slots, source well, and dispense volume
- Ends with `pipette.drop_tip()` so no tip remains attached

Use this workflow when:
- The user wants an example Opentrons workflow
- The task mentions making a `P` shape, letter pattern, or well-plate pattern using aspirate and dispense
- The workflow should demonstrate direct Opentrons liquid handling rather than optimization

Before running:
- Refer to: [example P shape](references/example/p-shape.md)
- Protocol generator: [scripts/example/p_shape.py](scripts/example/p_shape.py)
- Machine reference: [opentrons machine](../machine/references/opentrons-machine.md)
- Ask the user to confirm all deck slots before generating or running the protocol

## Critical Rules

1. Ask the user for source labware, destination labware, tip rack, pipette, mount, deck slots, source well, and dispense volume before generating a runnable protocol.
2. Do not assume deck slots.
3. Use explicit `pipette.aspirate(...)` and `pipette.dispense(...)` calls for the P-shape workflow; do not replace them with `transfer()` or `distribute()`.
4. Opentrons protocols must always end with no tip attached.
5. Do not run robot movement unless the user explicitly approves execution.
