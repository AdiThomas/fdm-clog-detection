# Early Detection and Correction of Nozzle Clogs in Desktop 3D Printers

ENGG*4000 capstone design project, University of Guelph (Group 51, Fall 2026).
Team: Aditya Thomas, Ahsan Minhas, Mohammad Moosa Basit and Ainsley Williams.
Client: University of Guelph 3D Printing Lab (advisor Prof. Singh as client representative).

> **Status: proposal stage.** The proposal was submitted on November 6, 2026. Nothing has
> been built yet. This repository will hold the firmware, analysis and hardware files as
> the build starts.

## The problem

On a desktop FDM printer, filament is melted in the hotend and pushed through a nozzle
about 0.4 mm wide. Standard printers run open-loop: they follow the G-code without
checking that plastic is actually coming out. A clog usually builds up gradually (heat
creep, debris, degraded polymer, or asking for more flow than the hotend can melt), and
nobody notices until under-extrusion shows up in the part. On a long unattended print,
that can mean hours of wasted time, filament and energy.

## What we're building

An add-on for an existing printer that:

1. detects a developing nozzle clog,
2. decides whether it can recover,
3. applies a safe corrective action, and
4. otherwise pauses the print and alerts the user,

while logging each clog event for quality assessment.

**Scope:** one direct-drive FDM printer running [Klipper](https://www.klipper3d.org/),
PLA, a 0.4 mm nozzle and gradually developing partial clogs. PETG is a stretch goal.
Hard blockages, unrelated print failures, multi-material printing, other printers and
commercialization are out of scope.

## Success criteria

| Criterion | Target |
| --- | --- |
| Warning lead time | Alert at least **5 minutes** before the first visible defect |
| Recovery | At least **70%** of recoverable clog runs finish with no visible defect |
| False alarms | No more than **1 in 10** normal prints interrupted unnecessarily |
| Filament waste | At least **50%** less filament wasted on clog runs than with no intervention |
| Part quality | Recovered parts within **5%** of the mass of a defect-free reference part |
| Response time | Condition assessed at least once per second; command sent within **2 s** of a decision |
| Hardware cost | Under **$400** per printer |
| Installation | A technician can install and calibrate it in under **3 hours** |

## Constraints

- The firmware's thermal-runaway protection stays enabled and independent of this system.
  It is checked before every test, and nothing this system sends can disable it.
- Corrective actions never heat the hotend past the filament's maximum rated temperature.
- All added electronics run on fused low-voltage DC (the printer's 24 V or a certified
  5 V adapter). No mains wiring is touched.
- No mainboard replacement, and no change to the user's slicer workflow.
- Hardware and materials within the $385 allowance.
- Tested and demonstrated within the 12-week ENGG*41x0 term.

## Approach

The team follows a Waterfall process (analysis, design, development, testing,
implementation), with feedback allowed only to the previous phase.

Concept generation starts from the six sensing families found in the literature, with
none chosen yet:

- filament motion sensing
- vision-based monitoring
- nozzle vibration
- extruder motor current
- acoustic emission
- extrusion force (load cell)

Clogs are induced under supervision (for example by feeding faster than the hotend can
melt, or by fitting a smaller nozzle). Baseline runs with no intervention are the
reference for relative targets such as filament saved.

## Repository layout

```
docs/proposal/   the submitted proposal (ENGG4000_Proposal_F26_Gr51.docx)
firmware/        Klipper configuration and macros, monitoring service (to come)
analysis/        sensor logs, notebooks, baseline and test results (to come)
hardware/        sensor mounts, wiring diagrams, bill of materials (to come)
```

## Roadmap

- [x] Proposal submitted (November 6, 2026)
- [ ] Client approval and confirmed requirements
- [ ] User questionnaire at campus makerspaces
- [ ] Baseline runs: confirm the chosen signal gives a clear early warning
- [ ] Concept selection
- [ ] Prototype: sensing, detection, correction, pause and alert
- [ ] Verification against every criterion and constraint
- [ ] Final demonstration and report
