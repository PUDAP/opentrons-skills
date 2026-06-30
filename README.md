# Opentrons Skills

A local repository of PUDA skills for Opentrons OT-2 machine operation and example workflow generation.

## Overview

This repository contains skills following the Agent Skills structure. Each skill lives in its own folder with a required `SKILL.md` and optional `references/` or `scripts/` resources.

These skills help agents understand Opentrons machine capabilities, generate PUDA-compatible OT-2 protocols, validate liquid-handling sequencing, and use example workflows.

## Skill Modules

| Skill | Description |
|---|---|
| [machine](machine/) | Opentrons OT-2 machine skill for labware loading, pipette setup, tip handling, aspirate/dispense/transfer commands, protocol generation, CSV-driven loops, and camera capture. |
| [workflow](workflow/) | Opentrons workflow skill for reusable workflow examples, including a P-shaped well-plate pattern generated with explicit aspirate and dispense operations. |

## Machine Skill

The `machine` skill covers PUDA-connected Opentrons OT-2 usage.

| Machine | Machine ID | Description |
|---|---|---|
| Opentrons OT-2 | `opentrons` | Automated liquid handling and full protocol generation, including labware setup, pipetting, flow control, CSV-driven loops, custom labware, and camera capture. |

Before generating Opentrons commands, load:

- [machine/SKILL.md](machine/SKILL.md)
- [machine/references/opentrons-machine.md](machine/references/opentrons-machine.md)

## Workflow Skill

The `workflow` skill currently includes:

| Workflow | Description |
|---|---|
| Example P Shape (`example`) | Generates an OT-2 Python protocol that dispenses liquid into selected wells to form the letter `P` on a 96-well plate. |

Workflow resources:

- [workflow/SKILL.md](workflow/SKILL.md)
- [workflow/references/p-shape.md](workflow/references/p-shape.md)
- [workflow/scripts/p_shape.py](workflow/scripts/p_shape.py)

## Example P-Shape Protocol

Generate a sample protocol after confirming deck slots and labware:

```bash
python workflow/scripts/p_shape.py --source-slot 2 --dest-slot 3 --tiprack-slot 11 --source-labware-type nest_12_reservoir_15ml --volume-ul 20
```

The generated protocol uses explicit `pipette.aspirate(...)` and `pipette.dispense(...)` calls and ends with no tip attached.

## Critical Rules

- Do not assume Opentrons deck slots; ask the user to confirm them.
- Validate pipette, labware, source well, destination plate, tip rack, and dispense volume before generating runnable protocols.
- Use explicit aspirate/dispense calls for the P-shape workflow; do not replace them with `transfer()` or `distribute()`.
- Do not run robot movement unless the user explicitly approves execution.
