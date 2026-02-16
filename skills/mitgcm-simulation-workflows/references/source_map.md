# MITgcm source map: Simulation Workflows

Use this map after topic docs in `references/doc_map.md` for run-loop, checkpoint, and restart behavior.

## Fast source navigation
- `rg -n "pickup|checkpoint|nIter0|the_main_loop|forward_step|runclock" model/src pkg/runclock`
- `rg -n "SUBROUTINE (THE_MODEL_MAIN|THE_MAIN_LOOP|FORWARD_STEP|WRITE_PICKUP|READ_PICKUP|RUNCLOCK_)" model/src pkg/runclock`

## Suggested source entry points
- `model/src/the_model_main.F` | top-level simulation orchestration.
- `model/src/the_main_loop.F` | main run loop logic.
- `model/src/main_do_loop.F` | control flow around loop execution.
- `model/src/forward_step.F` | per-step call sequencing.
- `model/src/timestep.F` | timestep kernel.
- `model/src/do_the_model_io.F` | runtime output/checkpoint scheduling.
- `model/src/do_write_pickup.F` | checkpoint write trigger path.
- `model/src/write_pickup.F` | pickup file write implementation.
- `model/src/read_pickup.F` | pickup restore implementation.
- `model/src/check_pickup.F` | pickup consistency checks.
- `model/src/turnoff_model_io.F` | controlled output shutdown path.
- `pkg/runclock/runclock_readparms.F` | runclock configuration parsing.
- `pkg/runclock/runclock_continue.F` | run continuation condition checks.
- `pkg/runclock/runclock_gettime.F` | wall-clock tracking for runtime limits.

## Function-level behavior checks
- Verify restart flow order: `READ_PICKUP` -> `CHECK_PICKUP` -> `FORWARD_STEP`.
- Confirm checkpoint cadence by tracing `DO_WRITE_PICKUP` and `WRITE_PICKUP` against configured frequencies.
- For wall-clock-limited runs, inspect `RUNCLOCK_*` decisions before assuming physics instability.
