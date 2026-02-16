---
name: mitgcm-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Examples and Tutorials

## High-Signal Playbook

### Route conditions
- Use this skill when users ask which tutorial to start from, how to run documented example families, or how to compare method variants with reference outputs (docs: `doc/examples/examples.rst`).
- Route compilation/AD toolchain failures to `mitgcm-build-and-install`.
- Route forcing/package design details to `mitgcm-inputs-and-modeling`.
- Route log/diagnostics parsing and acceptance checks to `mitgcm-analysis-and-output`.

### Triage questions
- Is the user goal basic onboarding, method comparison (advection schemes), package demo, or adjoint workflow?
- Which tutorial branch is closest: barotropic, baroclinic, reentrant channel, deep convection, tracer advection, CFC offline, plume-on-slope?
- Which runtime budget/hardware mode is available (serial vs MPI)?
- Are package switches required (`ptracers`, `zonal_filt`, `opps`, `ggl90`, etc.)?
- Is the user validating against `results/output*.txt` or only generating exploratory runs?
- Are they comparing primary vs secondary `input.*` variants?

### Canonical workflow
1. Select tutorial from `doc/examples/examples.rst` by objective and prerequisites.
2. Follow case-local README compile/run sequence in `verification/tutorial_*`.
3. Run primary setup first and compare to `results/output.txt`.
4. Then run documented secondary setups (`input.*`) to isolate method/physics differences.
5. For tracer-advection comparisons, enable `ptracers` and set advection-related flags in `input/data` and `input/data.ptracers` (docs: `doc/examples/advection_in_gyre/advection_in_gyre.rst`).
6. Capture diagnostics and compare scheme behavior (conservation, diffusion, extrema) to documented expectations.

### Minimal working example
```bash
cd verification/tutorial_cfc_offline/build
../../../tools/genmake2 -mods ../code
make depend
make

cd ../run
ln -s ../input/* .
./prepare_run
../build/mitgcmuv > output.txt
```
```bash
# simpler offline (no CFC) variant
cd verification/tutorial_cfc_offline/run
rm -f *
ln -s ../input_tutorial/* .
ln -s ../input/* .
./prepare_run
../build/mitgcmuv > output.tut
```

### Pitfalls and fixes
- Missing variant-link order in run directory can mask intended `input.*` overrides; link variant first, base input second (docs: `doc/examples/examples.rst`).
- `ptracers` tutorial run without enabling `ptracers` in `code/packages.conf` leaves tracer pathway inactive (docs: `doc/examples/advection_in_gyre/advection_in_gyre.rst`).
- SOM tracer cases missing `PTRACERS_ALLOW_DYN_STATE` option produce inconsistent behavior (docs: `doc/examples/advection_in_gyre/advection_in_gyre.rst`).
- Deep-convection timestep set too aggressively; tutorial guidance uses conservative `deltaT` against advective stability bound (docs: `doc/examples/deep_convection/deep_convection.rst`).
- Assuming package docs imply automatic activation: `zonal_filt`, `opps`, and `ggl90` examples still require selecting the documented verification setups (docs: `doc/phys_pkgs/zonal_filt.rst`, `doc/phys_pkgs/opps.rst`, `doc/phys_pkgs/ggl90.rst`).
- Comparing outputs without checking solver tolerances (`cg2dTargetResidual`) can misclassify runs as physics differences.

### Convergence and validation checks
- Confirm final `Iter.Nb` and diagnostics-list counts match case reference output.
- Confirm `cg2d_last_res` remains within target regime and does not drift upward during long runs.
- For advection tutorial, compare extrema/variance behavior across schemes as documented (dispersion/diffusion/positivity trade-offs).
- For deep-convection-like setups, verify stable integration without spurious blow-up at selected timestep.
- Keep at least one known-good baseline output per tutorial branch before modifying methods.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/phys_pkgs/cal.rst`
- `verification/tutorial_reentrant_channel/results/output.txt`
- `verification/tutorial_held_suarez_cs/results/output.txt`
- `doc/phys_pkgs/aim.rst`
- `verification/tutorial_deep_convection/results/output.txt`
- `verification/tutorial_deep_convection/results/output.smag3d.txt`
- `verification/tutorial_baroclinic_gyre/results/output.txt`
- `verification/tutorial_advection_in_gyre/results/output.txt`
- `verification/cfc_example/results/output.txt`
- `doc/phys_pkgs/zonal_filt.rst`
- `doc/phys_pkgs/opps.rst`
- `doc/phys_pkgs/ggl90.rst`

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
- `pkg/zonal_filt/zonal_filter.F`
- `pkg/zonal_filt/zonal_filt_readparms.F`
- `pkg/zonal_filt/zonal_filt_apply_ts.F`
- `pkg/ptracers/ptracers_zonal_filt_apply.F`
- `pkg/opps/opps_calc.F`
- `pkg/ggl90/ggl90_output.F`
- `pkg/ggl90/ggl90_calc_visc.F`
- `pkg/tapenade/stubs_tap_tlm.F`
- `pkg/tapenade/stubs_tap_adj.F`
- `pkg/tapenade/COST_TAP_TLM.h`
- `pkg/shap_filt/shap_filt_tracer_s4.F`
- `pkg/aim_v23/aim_write_phys.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
