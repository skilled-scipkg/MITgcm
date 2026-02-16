# MITgcm source map: Build and Install

Use this map after the topic docs in `references/doc_map.md` when compile/link workflows fail.

## Fast source navigation
- `rg -n "-mpi|-omp|-tap|-mods|-of" tools/genmake2 verification/testreport`
- `rg -n "autodiff|tapenade|depend|Makefile" tools eesupp pkg/autodiff pkg/tapenade pkg/offline`

## Suggested source entry points
- `tools/genmake2` | primary build-configuration generator.
- `tools/f90mkdepend` | Fortran dependency scanner used by build scripts.
- `tools/suggest_optfile_names` | optfile selection helper.
- `eesupp/src/Makefile` | executable link orchestration.
- `eesupp/inc/DEF_IN_MAKEFILE.h` | preprocessor definitions injected by build.
- `lsopt/Makefile` | platform/optimization options integration.
- `model/src/model_ad_diff.list` | AD dependency list for sensitivity builds.
- `pkg/autodiff/autodiff_readparms.F` | AD runtime control parsing.
- `pkg/autodiff/autodiff_ini_model_io.F` | AD I/O setup path.
- `pkg/tapenade/stubs_tap_tlm.F` | Tapenade TLM entry stubs.
- `pkg/tapenade/stubs_tap_adj.F` | Tapenade adjoint entry stubs.
- `pkg/offline/offline_readparms.F` | offline package runtime parsing.
- `pkg/offline/offline_fields_load.F` | offline forcing-field ingestion.
- `verification/testreport` | end-to-end compile/run regression harness.

## Function-level behavior checks
- Validate `genmake2` flags (`-mpi`, `-omp`, `-tap`, `-mods`) against generated `Makefile` definitions.
- For AD/TLM builds, confirm `AUTODIFF_READPARMS` and Tapenade stubs are linked into the requested target.
- For offline cases, verify `OFFLINE_READPARMS` values are consumed before `OFFLINE_FIELDS_LOAD` executes.
