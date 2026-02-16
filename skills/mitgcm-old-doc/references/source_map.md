# MITgcm source map: Old Doc

Use this map after legacy docs in `references/doc_map.md` when old option names must be mapped to current code paths.

## Fast source navigation
- `rg -n "diag|diagnostics|obcs|open boundary|legacy|changes" model/src pkg/diagnostics pkg/obcs pkg/exf pkg/land`
- `rg -n "SUBROUTINE (DO_STATEVARS_DIAGS|DIAGNOSTICS|OBCS_)" model/src pkg/diagnostics pkg/obcs`

## Suggested source entry points
- `model/src/do_statevars_diags.F` | main state diagnostics driver.
- `pkg/diagnostics/diagnostics_readparms.F` | diagnostics parameter parsing.
- `pkg/diagnostics/diagnostics_setdiag.F` | diagnostics registration wiring.
- `pkg/diagnostics/diagstats_calc.F` | legacy-to-current diag statistics logic.
- `pkg/diagnostics/diagstats_output.F` | diagnostics statistics output path.
- `pkg/obcs/obcs_readparms.F` | open-boundary option parsing.
- `pkg/obcs/obcs_check.F` | open-boundary consistency checks.
- `pkg/obcs/obcs_apply_ts.F` | tracer open-boundary application.
- `pkg/obcs/obcs_apply_uv.F` | velocity open-boundary application.
- `pkg/obcs/obcs_fields_load.F` | open-boundary field loading.
- `pkg/land/land_do_diags.F` | package diagnostics integration example.
- `pkg/exf/exf_weight_sfx_diags.F` | forcing-diagnostics weighting path.

## Function-level behavior checks
- Map old diagnostics labels to current `DIAGNOSTICS_SETDIAG` registrations before changing configs.
- For OpenBound migration work, compare `OBCS_READPARMS` values with downstream `OBCS_APPLY_TS`/`OBCS_APPLY_UV` usage.
- Validate legacy diagnostics expectations against modern `DIAGSTATS_CALC` and `DIAGSTATS_OUTPUT` behavior.
