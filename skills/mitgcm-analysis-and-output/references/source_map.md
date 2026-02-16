# MITgcm source map: Analysis and Output

Use this map after the topic docs in `references/doc_map.md` when stdout/diagnostic behavior is ambiguous.

## Fast source navigation
- `rg -n "Iter\.Nb|cg2d_last_res|diagnostics|monitor" model/src pkg/diagnostics pkg/monitor pkg/mnc`
- `rg -n "SUBROUTINE (DIAGNOSTICS|DIAGSTATS|MONITOR|WRITE_PICKUP)" model/src pkg/diagnostics pkg/monitor`

## Suggested source entry points
- `model/src/do_the_model_io.F` | top-level model output scheduling.
- `model/src/do_statevars_diags.F` | state-variable diagnostics generation.
- `model/src/write_state.F` | binary state output write path.
- `model/src/write_pickup.F` | checkpoint file write behavior.
- `pkg/diagnostics/diagnostics_main_init.F` | diagnostics package bootstrap.
- `pkg/diagnostics/diagnostics_readparms.F` | diagnostics namelist parsing.
- `pkg/diagnostics/diagnostics_out.F` | diagnostics output dispatch.
- `pkg/diagnostics/diagnostics_write.F` | diagnostics file write logic.
- `pkg/diagnostics/diagstats_calc.F` | online statistics calculations.
- `pkg/diagnostics/diagstats_output.F` | diagstats output rendering.
- `pkg/mnc/mnc_dump.F` | MNC output dump path.
- `pkg/mnc/mnc_update_time.F` | MNC time axis updates.
- `pkg/monitor/monitor.F` | `%MON` monitor line generation.

## Function-level behavior checks
- Verify `DIAGNOSTICS_READPARMS` -> `DIAGNOSTICS_MAIN_INIT` ordering before expecting diagnostic fields.
- Check that `WRITE_PICKUP` cadence aligns with `pChkptFreq` and restart expectations.
- Trace `%MON` values by following `MONITOR` calls near timestep loops and compare with `output.txt` lines.
