---
name: mitgcm-simulation-workflows
description: This skill should be used when users ask about simulation workflows in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Simulation Workflows

## High-Signal Playbook

### Route conditions
- Use this skill for run sequencing, checkpoint/restart policy, long integrations, and wall-clock-limited workflow design.
- Route compile/toolchain issues to `mitgcm-build-and-install`.
- Route forcing/package setup to `mitgcm-inputs-and-modeling`.
- Route diagnostics interpretation to `mitgcm-analysis-and-output`.

### Triage questions
- Is this a fresh run, pickup restart, or branch run from an intermediate checkpoint?
- Which run-control values matter (`nIter0`, `endTime`, checkpoint/output frequencies)?
- Is wall-clock continuation required (`runclock` package)?
- Are there multiple input overlays (`input.*`) and do they change restart behavior?
- What is the validation target (`results/output*.txt`, pickup continuity, monitor continuity)?

### Canonical workflow
1. Start from a verification case with explicit run instructions and reference output.
2. Build executable once, then treat `run/` as the workflow state machine.
3. Run a short baseline integration and confirm expected outputs/monitor diagnostics.
4. Enable pickup cadence and verify `pickup.*.meta/.data` files are produced.
5. Restart from pickup (`nIter0` and input settings aligned) and confirm continuity in diagnostics.
6. For production workflows, add runclock/walltime controls and checkpoint often enough for queue preemption.

### Minimal working example
```bash
cd verification/tutorial_barotropic_gyre/build
../../../tools/genmake2 -mods ../code
make depend
make

cd ../run
ln -s ../input/* .
../build/mitgcmuv > output.0000.txt
ls pickup.*.meta pickup.*.data
```
```bash
# restart continuity check
../build/mitgcmuv > output.restart.txt
rg -n "nIter0|pickup|Iter.Nb|cg2d_last_res" output.restart.txt
```

### Pitfalls and fixes
- Restart run with inconsistent `nIter0` or missing pickup files leads to silent cold-start behavior.
- Disabling output/checkpoint frequencies for long runs removes recovery points after queue preemption.
- Mixing `input.*` overlays between baseline and restart creates false discontinuities.
- Assuming wall-clock exits are model failures; check runclock stop condition first.

### Convergence and validation checks
- Baseline and restart runs should show continuous iteration/time progression.
- Pickup files should appear at expected cadence and be readable by restart run.
- Key diagnostics (`Iter.Nb`, `cg2d_last_res`, monitor streams) should remain continuous across restart boundary.
- Final output should remain comparable to chosen reference result for the selected setup.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/getting_started/getting_started.rst`
- `doc/algorithm/crank-nicol.rst`
- `verification/tutorial_barotropic_gyre/README.md`
- `verification/tutorial_baroclinic_gyre/README.md`
- `verification/front_relax/README.md`
- `verification/offline_exf_seaice/README`
- `verification/1D_ocean_ice_column/README_11K_TIME_STEP_SIMULATION.TXT`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `verification`
- `doc/examples`
- `tools/example_scripts`
- `utils/python/MITgcmutils/MITgcmutils/examples`

## Test references
- `verification`

## Optional deeper inspection
- `eesupp`
- `lsopt`
- `model`
- `optim`
- `pkg`
- `tools`
- `utils/python/MITgcmutils/MITgcmutils`

## Source entry points for unresolved issues
- `model/src/the_model_main.F`
- `model/src/the_main_loop.F`
- `model/src/main_do_loop.F`
- `model/src/forward_step.F`
- `model/src/timestep.F`
- `model/src/do_the_model_io.F`
- `model/src/do_write_pickup.F`
- `model/src/write_pickup.F`
- `model/src/read_pickup.F`
- `model/src/check_pickup.F`
- `model/src/turnoff_model_io.F`
- `pkg/runclock/runclock_readparms.F`
- `pkg/runclock/runclock_continue.F`
- `pkg/runclock/runclock_gettime.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
