# MITgcm source map: Getting Started

Use this map after the topic docs in `references/doc_map.md` when first-run behavior is unclear.

## Fast source navigation
- `rg -n "initial|packages_readparms|forward_step|timestep|output" model/src eesupp/src tools/genmake2`
- `rg -n "SUBROUTINE (THE_MODEL_MAIN|INITIALISE|INI_PARMS|FORWARD_STEP|TIMESTEP)" model/src`

## Suggested source entry points
- `tools/genmake2` | initial build configuration script used by almost all starter cases.
- `eesupp/src/eeboot.F` | execution-environment startup sequence.
- `model/src/the_model_main.F` | high-level model entry point.
- `model/src/main_do_loop.F` | driver loop setup before time stepping.
- `model/src/initialise_fixed.F` | fixed-configuration initialization.
- `model/src/initialise_varia.F` | runtime-variable initialization.
- `model/src/ini_parms.F` | namelist and parameter load path.
- `model/src/packages_readparms.F` | package parameter ingestion.
- `model/src/packages_check.F` | package consistency checks.
- `model/src/forward_step.F` | forward-step sequencing.
- `model/src/timestep.F` | timestep update kernel.
- `model/src/do_the_model_io.F` | output scheduling for first validation.
- `model/src/config_summary.F` | startup summary block content.

## Function-level behavior checks
- Verify startup order: `THE_MODEL_MAIN` -> initialization routines -> `FORWARD_STEP`.
- If package flags do not apply, trace `PACKAGES_READPARMS` and `PACKAGES_CHECK` for rejection messages.
- Map missing/extra startup log lines in `output.txt` to `CONFIG_SUMMARY` and `DO_THE_MODEL_IO` calls.
