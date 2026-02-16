---
name: mitgcm-build-and-install
description: This skill should be used when users ask about build and install in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Build and Install

## High-Signal Playbook

### Route conditions
- Use this skill for compile/link failures, `genmake2` usage, optfile selection, and forward/adjoint/TLM executable generation (docs: `doc/getting_started/getting_started.rst`, `verification/tutorial_barotropic_gyre/README.md`, `doc/autodiff/autodiff.rst`).
- Route experiment physics/forcing setup to `mitgcm-inputs-and-modeling`.
- Route algorithmic stability/timestep questions to `mitgcm-theory-and-methods`.
- Route run result interpretation and diagnostics parsing to `mitgcm-analysis-and-output`.

### Triage questions
- Which target executable is needed: `mitgcmuv`, `mitgcmuv_ad`, `mitgcmuv_tap_tlm`, or `mitgcmuv_tap_adj` (docs: `doc/autodiff/autodiff.rst`)?
- Which experiment directory and code overlay (`code`, `code_ad`, `code_tap`) is being built?
- Serial build, MPI (`-mpi`), or OpenMP (`-omp`) (docs: `doc/getting_started/getting_started.rst`)?
- Which compiler/optfile is in use (`-of my_platform_optionFile`)?
- Is `prepare_run` required before execution (e.g., offline/CFC workflows) (docs: `verification/tutorial_cfc_offline/README.md`)?
- Forward-only, adjoint regression, or Tapenade generation target?

### Canonical workflow
1. Enter a `verification/<case>/build` directory and run `../../../tools/genmake2 -mods ../code [-of ...]`.
2. Run `make depend` then `make` (or `make adall`, `make tap_tlm`, `make tap_adj` depending on target) (docs: `doc/autodiff/autodiff.rst`).
3. Enter `run/`, link input files, run `prepare_run` if present, and execute compiled binary (docs: `verification/tutorial_cfc_offline/README.md`).
4. Compare against `results/output*.txt` for quick acceptance.
5. For adjoint: build with `../code_ad`, run with `../input_ad/*`, and compare `output_adm.txt` to reference (docs: `verification/global_ocean_ebm/README.md`).
6. For Tapenade: use `-tap`, then follow `tap_tlm` or `tap_adj` recipe from autodiff docs.

### Minimal working example
```bash
cd verification/tutorial_barotropic_gyre/build
../../../tools/genmake2 -mods ../code
make depend
make

cd ../run
ln -s ../input/* .
ln -s ../build/mitgcmuv .
./mitgcmuv > output.txt
```
```bash
cd verification/tutorial_cfc_offline/run
ln -s ../input/* .
./prepare_run
../build/mitgcmuv > output.txt
```

### Pitfalls and fixes
- Missing `make depend` before `make` can leave stale dependencies unresolved (docs: tutorial READMEs in `verification/tutorial_*`).
- Wrong code overlay (`../code` vs `../code_ad` vs `../code_tap`) produces wrong executable set (docs: `doc/autodiff/autodiff.rst`).
- Offline/CFC run without `prepare_run` leaves required links/files absent (docs: `verification/tutorial_cfc_offline/README.md`).
- Divided adjoint not enabled when expected: set `USE_DIVA=1` (and matching AD options) before `adall` (docs: `doc/autodiff/autodiff.rst`, `verification/lab_sea/README.md`).
- Package enabled without matching AD file list may break AD generation; extend `package_ad_diff.list` as instructed (docs: `doc/autodiff/autodiff.rst`).
- Platform-dependent comparison drift: use documented reference outputs and tolerances before calling a regression failure.

### Convergence and validation checks
- Build should produce the intended executable in `build/` with no unresolved symbols.
- Startup banner in `output.txt` should show expected checkpoint/build metadata and requested runtime layout.
- `Iter.Nb`, diagnostics list counts, and cg2d residual behavior should be comparable to `results/output*.txt`.
- Adjoint/TLM runs should produce expected named outputs (`output_adm.txt`, `output_tap_tlm.txt`, `output_tap_adj.txt`) and reference comparability.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `verification/tutorial_cfc_offline/README.md`
- `verification/natl_box/README.md`
- `verification/tutorial_baroclinic_gyre/README.md`
- `verification/tutorial_reentrant_channel/README.md`
- `verification/tutorial_barotropic_gyre/README.md`
- `verification/flt_example/README.md`
- `doc/autodiff/autodiff.rst`
- `doc/examples/reentrant_channel/reentrant_channel.rst`
- `doc/examples/barotropic_gyre/barotropic_gyre.rst`
- `doc/examples/baroclinic_gyre/baroclinic_gyre.rst`
- `doc/old_doc/optfiles_changes.txt`

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
- `eesupp/src/Makefile`
- `eesupp/inc/DEF_IN_MAKEFILE.h`
- `lsopt/Makefile`
- `pkg/exch2/Makefile`
- `pkg/mnc/Makefile`
- `pkg/regrid/Makefile`
- `pkg/autodiff/autodiff_ini_model_io.F`
- `pkg/offline/offline_readparms.F`
- `pkg/offline/offline_fields_load.F`
- `pkg/cfc/cfc_fields_load.F`
- `pkg/flt/flt_main.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
