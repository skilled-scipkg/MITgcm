# MITgcm source map: Verification

Use this map after docs in `references/doc_map.md` when verification harness behavior or regression criteria are unclear.

## Fast source navigation
- `rg -n "usage\(|testoutput_|runmodel|match|cmp" verification/testreport verification/verification_parser.py`
- `rg -n "autodiff|tap|adj|tlm" pkg/autodiff pkg/tapenade tools`

## Suggested source entry points
- `verification/testreport` | primary regression harness (build/run/compare stages).
- `verification/verification_parser.py` | parser for verification experiment metadata.
- `tools/genmake2` | build flag expansion used by verification harness.
- `tools/do_tst_2+2` | quick distributed test utility.
- `model/src/config_summary.F` | startup config text used in regression outputs.
- `model/src/do_statevars_diags.F` | state diagnostics often compared in tests.
- `pkg/autodiff/autodiff_ini_model_io.F` | AD verification I/O initialization path.
- `pkg/autodiff/autodiff_store.F` | AD checkpoint/store behavior.
- `pkg/autodiff/autodiff_restore.F` | AD restore behavior.
- `pkg/tapenade/stubs_tap_tlm.F` | TLM verification stubs.
- `pkg/tapenade/stubs_tap_adj.F` | adjoint verification stubs.

## Function-level behavior checks
- In `verification/testreport`, trace `testoutput_run` and `testoutput_var` when pass/fail outcomes look suspicious.
- Confirm harness build flags passed to `genmake2` match intended MPI/AD/TAP mode.
- For AD/TLM regressions, inspect `AUTODIFF_*` and Tapenade stubs selected by target executable.
