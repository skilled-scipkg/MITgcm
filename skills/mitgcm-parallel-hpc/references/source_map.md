# MITgcm source map: Parallel and HPC

Use this map after the topic docs in `references/doc_map.md` for MPI/OpenMP decomposition, exchange, and scaling behavior.

## Fast source navigation
- `rg -n "nPx|nPy|usingMPI|threads|barrier|global_sum|exchange|timers" eesupp/src pkg/exch2 model/src`
- `rg -n "SUBROUTINE (INI_PROCS|BARRIER|GLOBAL_SUM|W2_|EXCH_)" eesupp/src pkg/exch2`

## Suggested source entry points
- `eesupp/src/ini_procs.F` | MPI process-grid initialization.
- `eesupp/src/ini_threading_environment.F` | OpenMP/thread setup.
- `eesupp/src/barrier.F` | synchronization barrier behavior.
- `eesupp/src/global_sum.F` | collective reduction behavior and scaling hotspot.
- `eesupp/src/comm_stats.F` | communication statistics and counters.
- `eesupp/src/timers.F` | timing instrumentation hooks.
- `eesupp/src/master_cpu_io.F` | single-master I/O behavior under MPI.
- `eesupp/src/exch_init.F` | exchange-pattern initialization.
- `pkg/exch2/w2_readparms.F` | EXCH2 decomposition parameter parsing.
- `pkg/exch2/w2_map_procs.F` | mapping tiles to MPI ranks.
- `pkg/exch2/w2_e2setup.F` | EXCH2 communication topology setup.
- `pkg/exch2/w2_print_comm_sequence.F` | explicit communication sequence tracing.
- `model/src/config_summary.F` | startup reporting of decomposition settings.
- `model/src/do_fields_blocking_exchanges.F` | blocking halo exchange behavior.
- `model/src/do_stagger_fields_exchanges.F` | staggered-grid halo exchange behavior.

## Function-level behavior checks
- Validate `nPx*nPy` and tile mapping by tracing `INI_PROCS` and `W2_MAP_PROCS` outputs.
- For halo mismatches, compare call paths through `EXCH_INIT` and the `DO_*_EXCHANGES` routines.
- Use timing and comm counters (`TIMERS`, `COMM_STATS`) to confirm scaling bottlenecks before tuning.
