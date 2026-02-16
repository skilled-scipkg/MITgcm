---
name: mitgcm-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Parallel and HPC

## High-Signal Playbook

### Route conditions
- Use this skill for MPI/OpenMP execution setup, decomposition (`nPx`, `nPy`, `sNx`, `sNy`), exchange behavior, and scaling/performance triage.
- Route physics/package configuration to `mitgcm-inputs-and-modeling`.
- Route compile/toolchain failures to `mitgcm-build-and-install`.
- Route restart/checkpoint policy to `mitgcm-simulation-workflows`.

### Triage questions
- Is this serial, MPI, OpenMP, or hybrid MPI+OpenMP?
- What decomposition is intended (`nPx*nPy` vs available cores/ranks)?
- Is this regular lat-lon, cubed sphere, or EXCH2 topology?
- Are failures correctness-related (hang, exchange mismatch) or throughput-related (slow scaling)?
- Are we validating a single short run first, then scaling out?

### Canonical workflow
1. Start from a known verification case with documented MPI behavior (`lab_sea`, `global_ocean.90x40x15`, or `cpl_aim+ocn`).
2. Build with MPI support (`../../../tools/genmake2 -mpi -mods ../code [-of <optfile>]`, then `make depend && make`).
3. Set runtime decomposition (`nPx`, `nPy`) to match rank count and tile layout constraints.
4. Run short smoke test (`mpirun -np N ../build/mitgcmuv > output.mpi.txt`) before long production runs.
5. Validate header and monitor diagnostics (`usingMPI`, decomposition summary, `cg2d` health, final `Iter.Nb`).
6. Scale ranks/threads gradually and compare throughput plus numerical comparability against baseline.

### Minimal working example
```bash
cd verification/lab_sea/build
../../../tools/genmake2 -mpi -mods ../code
make depend
make

cd ../run
ln -s ../input/* .
mpirun -np 2 ../build/mitgcmuv > output.mpi.txt
rg -n "usingMPI|nPx|nPy|Iter.Nb|cg2d_last_res" output.mpi.txt
```
```bash
# OpenMP-only run (if executable was built with -omp)
export OMP_NUM_THREADS=4
../build/mitgcmuv > output.omp.txt
```

### Pitfalls and fixes
- Rank count mismatch with decomposition (`nPx*nPy != -np`) causes immediate startup failures.
- Running MPI binary without MPI launcher or hostfile setup can silently hang on some systems.
- EXCH2/cubed-sphere cases need topology-consistent tile maps; avoid reusing decomposition from lat-lon runs.
- Comparing throughput before first correctness check hides configuration regressions.
- Master-only I/O can become bottleneck at large rank counts; validate I/O strategy before scaling.

### Convergence and validation checks
- Startup must report expected MPI mode and decomposition.
- Final `Iter.Nb`/`Time(s)` and key monitor diagnostics should remain comparable to reference outputs.
- `cg2d_last_res` and solver iteration trends should remain stable when increasing rank count.
- Scaling tests should report time-per-step improvement without changing configured physics/options.

## Scope
- Handle questions about MPI/OpenMP/GPU execution, scaling, and batch systems.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/getting_started/getting_started.rst`
- `doc/phys_pkgs/exch2.rst`
- `verification/lab_sea/README.md`
- `verification/global_ocean.90x40x15/README`
- `verification/global_ocean.cs32x15/README`
- `verification/cpl_aim+ocn/README.md`
- `verification/adjustment.cs-32x32x1/README`
- `verification/hs94.1x64x5/README`

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
- `eesupp/src/ini_procs.F`
- `eesupp/src/ini_threading_environment.F`
- `eesupp/src/barrier.F`
- `eesupp/src/global_sum.F`
- `eesupp/src/comm_stats.F`
- `eesupp/src/timers.F`
- `eesupp/src/master_cpu_io.F`
- `eesupp/src/exch_init.F`
- `pkg/exch2/w2_readparms.F`
- `pkg/exch2/w2_map_procs.F`
- `pkg/exch2/w2_e2setup.F`
- `pkg/exch2/w2_print_comm_sequence.F`
- `model/src/config_summary.F`
- `model/src/do_fields_blocking_exchanges.F`
- `model/src/do_stagger_fields_exchanges.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
