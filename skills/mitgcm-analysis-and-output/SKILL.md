---
name: mitgcm-analysis-and-output
description: This skill should be used when users ask about analysis and output in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Analysis and Output

## High-Signal Playbook

### Route conditions
- Use this skill for stdout diagnostics triage, reference-output comparison, and run-health checks from `output*.txt` files (docs: `verification/*/results/output*.txt`).
- Route output-generation parameter design to `mitgcm-inputs-and-modeling`.
- Route scheme/stability root-cause analysis to `mitgcm-theory-and-methods`.
- Route toolchain/build failures to `mitgcm-build-and-install`.

### Triage questions
- Which reference output file is authoritative for this run (`results/output.txt`, variant `output.*.txt`, or adjoint logs)?
- Is the request about startup configuration, iteration-time diagnostics, solver convergence, or package-specific monitors?
- Is this serial or MPI/cubed-sphere execution (check `usingMPI`, `nPx/nPy`, and exchange mode in header)?
- Which package diagnostics are expected (e.g., THSICE/SEAICE/SHELFICE monitor fields)?
- Are mismatches numerical drift, configuration mismatch, or wrong input variant?
- Is acceptance strict byte-level comparison or tolerance-based behavior matching?

### Canonical workflow
1. Confirm run identity from header (checkpoint, grid layout, MPI mode, tile mapping) in `output.txt`.
2. Locate final-time section (`Iter.Nb`, `Time(s)`, diagnostics list counts).
3. Inspect monitor lines (`%MON ...`) and cg2d convergence lines (`cg2d_init_res`, `cg2d_last_res`, iteration counts).
4. Compare with corresponding `verification/<case>/results/output*.txt` reference.
5. If mismatch, verify active namelist/runtime settings echoed in log (`monitorFreq`, `cg2dTargetResidual`, `nonlinFreeSurf`, etc.).
6. Escalate to package output routines in source when behavior differs but docs/logs are ambiguous.

### Minimal working example
```bash
../build/mitgcmuv > output.txt
rg -n "Iter.Nb|2D/3D diagnostics|%MON time_tsnumber|cg2d_last_res" output.txt
```
```bash
# compare with case reference diagnostics blocks
rg -n "Iter.Nb|2D/3D diagnostics|cg2d_last_res" results/output.txt
```

### Pitfalls and fixes
- Wrong `input.*` overlay leads to valid but non-comparable output profile; verify run setup before comparison (docs: tutorial READMEs and `doc/examples/examples.rst`).
- Assuming first `monitorFreq` assignment is active when later lines override it in namelist echo.
- Treating high `cg2d_iters` near `cg2dMaxIters` as acceptable noise; this usually signals pressure-solver stress.
- Comparing runs across different decomposition/precision settings (`usingMPI`, `readBinaryPrec`) without accounting for expected differences.
- Ignoring package-specific monitor streams (e.g., `thSI_time_sec`) when validating THSICE-enabled setups.
- Reading only startup header and missing final diagnostics-list counts that reveal incomplete/failed run state.

### Convergence and validation checks
- `Iter.Nb` and `Time(s)` should match expected endpoint from reference run.
- `2D/3D diagnostics: Number of lists` and global-stat diagnostics counts should match the selected setup.
- `cg2d_last_res` should remain below configured target scale; trend should not degrade over successive steps.
- `%MON time_secondsf` increments should align with configured timestep/output cadence.
- Package-specific monitor fields should appear when corresponding package/input options are active.

## Scope
- Handle questions about output formats, analysis, and post-processing.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `verification/ideal_2D_oce/results/output.txt`
- `verification/global_ocean.90x40x15/results/output.txt`
- `verification/global_ocean.90x40x15/results/output.dwnslp.txt`
- `verification/fizhi-cs-aqualev20/results/output.txt`
- `verification/atm_gray/results/output.txt`
- `verification/global_ocean.cs32x15/results/output.in_p.txt`
- `verification/global_ocean.cs32x15/results/output.thsice.txt`
- `verification/atm_gray/results/output.ape.txt`
- `verification/aim.5l_cs/results/output.thSI.txt`
- `verification/vermix/results/output.gglLC.txt`
- `verification/vermix/results/output.ggl90.txt`
- `verification/shelfice_2d_remesh/results/output.txt`

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
- `pkg/thsice/thsice_output.F`
- `pkg/thsice/thsice_get_ocean.F`
- `pkg/seaice/seaice_output.F`
- `pkg/seaice/seaice_obcs_output.F`
- `pkg/seaice/seaice_budget_ocean.F`
- `pkg/shelfice/shelfice_output.F`
- `pkg/shelfice/shelfice_remesh_state.F`
- `pkg/fizhi/update_ocean_exports.F`
- `pkg/aim_v23/phy_suflux_post.F`
- `pkg/atm_compon_interf/atm_store_aim_fields.F`
- `pkg/atm_compon_interf/cpl_output.F`
- `pkg/ggl90/ggl90_output.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
