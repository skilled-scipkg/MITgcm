---
name: mitgcm-getting-started
description: This skill should be used when users ask about getting started in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Getting Started

## High-Signal Playbook

### Route conditions
- Use this skill when the user needs a first runnable MITgcm case, a forward/adjoint starter path, or experiment selection from `verification/*` (docs: `doc/overview/overview.rst`, `verification/front_relax/README.md`, `verification/lab_sea/README.md`).
- Route build-toolchain failures to `mitgcm-build-and-install` (docs: `verification/tutorial_barotropic_gyre/README.md`, `doc/getting_started/getting_started.rst`).
- Route package-specific namelist/forcing design to `mitgcm-inputs-and-modeling` (docs: `doc/phys_pkgs/phys_pkgs.rst`, `doc/phys_pkgs/ptracers.rst`).
- Route coupler/MPI scaling details to `mitgcm-parallel-hpc` and restart/checkpoint policy to `mitgcm-simulation-workflows`.

### Triage questions
- Which starting experiment is closest to target physics: `front_relax`, `lab_sea`, `cpl_aim+ocn`, `tutorial_plume_on_slope`, or `solid-body.cs-32x32x1` (docs: corresponding `verification/*/README*`)?
- Forward-only or adjoint/TLM workflow (docs: `verification/lab_sea/README.md`, `verification/global_ocean_ebm/README.md`)?
- Serial or MPI run (docs: `verification/lab_sea/README.md`, `verification/cpl_aim+ocn/README.md`)?
- Is there a secondary setup (`input.*`) to overlay on top of `input/` (docs: `verification/front_relax/README.md`, `verification/lab_sea/README.md`)?
- Which reference output file is the acceptance target (`results/output*.txt`, `results/output_adm.txt`, `results/atmSTDOUT.*`)?
- Are sea-ice/coupler packages required from day one (docs: `verification/lab_sea/README.md`, `verification/cpl_aim+ocn/README.md`)?

### Canonical workflow
1. Pick one verification case with documented commands and reference output.
2. Build in `build/` using `../../../tools/genmake2 -mods ../code` (or `../code_ad`) then `make depend && make` (docs: `verification/front_relax/README.md`, `verification/lab_sea/README.md`, `verification/global_ocean_ebm/README.md`).
3. In `run/`, symlink `../input/*` (or `../input.$sc/*` first for variants), then run `prepare_run` only when the case requires it (docs: `verification/front_relax/README.md`, `verification/atm_gray/README.md`).
4. Run executable (`../build/mitgcmuv`, `./mitgcmuv`, or `mpirun -np N ../build/mitgcmuv`) (docs: `verification/lab_sea/README.md`).
5. Compare output to `results/output*.txt` and inspect monitor/cg2d blocks in stdout.
6. For adjoint, switch to `code_ad` + `input_ad`, run `prepare_run`, then `mitgcmuv_ad` (docs: `verification/lab_sea/README.md`, `verification/global_ocean_ebm/README.md`).

### Minimal working example
```bash
cd verification/lab_sea/build
../../../tools/genmake2 -mods ../code
make depend
make

cd ../run
ln -s ../input/* .
ln -s ../build/mitgcmuv .
./mitgcmuv > output.txt
```
```bash
cd verification/lab_sea/run
ln -s ../input_ad/* .
../input_ad/prepare_run
ln -s ../build/mitgcmuv_ad .
./do_run.sh
```

### Pitfalls and fixes
- `input.$sc` overlay order reversed: link `input.$sc/*` first, then `input/*`, so case-specific files are not overwritten (docs: `verification/front_relax/README.md`).
- Skipping required `prepare_run` step: required for some setups (`bvp`, adjoint inputs, atm_gray spin-up variants) (docs: `verification/front_relax/README.md`, `verification/lab_sea/README.md`, `verification/atm_gray/README.md`).
- P-coordinate vs Z-coordinate output mismatch in `front_relax`: flip vertical index and compare documented variable transforms (`Eta` vs `PHL`) (docs: `verification/front_relax/README.md`).
- Coupled setup launched without helper script sequence: use `tools/run_cpl_test` steps 1-3 (and 4 for compare) (docs: `verification/cpl_aim+ocn/README.md`).
- Adjoint build/run without divided-adjoint settings in `lab_sea`: honor `USE_DIVA` and `ALLOW_DIVIDED_ADJOINT` guidance (docs: `verification/lab_sea/README.md`).
- Cross-platform `testreport` differences interpreted as hard failures: check documented tolerance note for `lab_sea.hb87` (docs: `verification/lab_sea/README.md`).

### Convergence and validation checks
- Startup block must show intended grid decomposition (`nPx/nPy/nSx/nSy`) and execution mode (`usingMPI`) in `output.txt`.
- Final log should include expected `Iter.Nb`/`Time(s)` and `2D/3D diagnostics: Number of lists` for the chosen reference run.
- `cg2d_last_res` should remain below configured target scale (`cg2dTargetResidual` or `cg2dTargetResWunit`) for stable pressure solves.
- Output file comparison should match documented reference file for that setup (`results/output.txt`, `results/output.$sc.txt`, `results/output_adm.txt`).

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `verification/front_relax/README.md`
- `verification/global_ocean_ebm/README.md`
- `verification/lab_sea/README.md`
- `verification/global_oce_latlon/README.md`
- `verification/tutorial_plume_on_slope/README.md`
- `verification/solid-body.cs-32x32x1/README.md`
- `doc/overview/overview.rst`
- `verification/exp4/README.md`
- `verification/atm_gray/README.md`
- `verification/cpl_aim+ocn/README.md`
- `doc/phys_pkgs/ptracers.rst`
- `doc/phys_pkgs/phys_pkgs.rst`

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
- `tools/genmake2`
- `eesupp/src/eeboot.F`
- `model/src/the_model_main.F`
- `model/src/main_do_loop.F`
- `model/src/initialise_fixed.F`
- `model/src/initialise_varia.F`
- `model/src/ini_parms.F`
- `model/src/packages_readparms.F`
- `model/src/packages_check.F`
- `model/src/forward_step.F`
- `model/src/timestep.F`
- `model/src/do_the_model_io.F`
- `model/src/config_summary.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
