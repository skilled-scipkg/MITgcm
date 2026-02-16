# MITgcm source map: Examples and Tutorials

Use this map after reading tutorial docs in `references/doc_map.md` when setup behavior differs from expectations.

## Fast source navigation
- `rg -n "readparms|output|calc|forcing" model/src pkg/ptracers pkg/zonal_filt pkg/opps pkg/ggl90 pkg/cfc pkg/offline`
- `rg -n "SUBROUTINE (PTRACERS|ZONAL|OPPS|GGL90|CFC|OFFLINE)" pkg/ptracers pkg/zonal_filt pkg/opps pkg/ggl90 pkg/cfc pkg/offline`

## Suggested source entry points
- `model/src/packages_readparms.F` | package enable/disable gate used by tutorial cases.
- `model/src/do_statevars_diags.F` | standard diagnostics emitted in tutorial outputs.
- `pkg/ptracers/ptracers_readparms.F` | tracer configuration parsing.
- `pkg/ptracers/ptracers_forcing_surf.F` | tracer forcing behavior in tutorials.
- `pkg/zonal_filt/zonal_filt_readparms.F` | zonal filter runtime options.
- `pkg/zonal_filt/zonal_filter.F` | zonal filtering implementation.
- `pkg/opps/opps_readparms.F` | OPPS configuration parsing.
- `pkg/opps/opps_calc.F` | OPPS physics update.
- `pkg/ggl90/ggl90_readparms.F` | GGL90 setup options.
- `pkg/ggl90/ggl90_calc_visc.F` | GGL90 viscosity calculations.
- `pkg/cfc/cfc_readparms.F` | CFC package setup in offline tutorials.
- `pkg/offline/offline_readparms.F` | offline forcing/control configuration.
- `pkg/tapenade/stubs_tap_tlm.F` | tutorial TLM entry stubs.
- `pkg/tapenade/stubs_tap_adj.F` | tutorial adjoint entry stubs.

## Function-level behavior checks
- Confirm tutorial package activation paths by tracing `PACKAGES_READPARMS` to package `*_READPARMS` routines.
- When outputs diverge, compare package `*_CALC` or forcing routines (`OPPS_CALC`, `GGL90_CALC_VISC`, `PTRACERS_FORCING_SURF`).
- For AD tutorial variants, confirm Tapenade stubs selected by build target match runtime executable.
