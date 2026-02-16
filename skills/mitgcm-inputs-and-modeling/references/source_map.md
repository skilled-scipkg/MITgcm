# MITgcm source map: Inputs and Modeling

Use this map after the topic docs in `references/doc_map.md` when input/forcing behavior does not match configuration.

## Fast source navigation
- `rg -n "readparms|load|forcing|obcs|seaice|exf|bulk" model/src pkg/exf pkg/bulk_force pkg/obcs pkg/seaice pkg/ptracers`
- `rg -n "SUBROUTINE (.*READPARMS|.*FIELDS_LOAD|.*MODEL)" pkg/exf pkg/bulk_force pkg/obcs pkg/seaice pkg/ptracers`

## Suggested source entry points
- `model/src/packages_readparms.F` | package-level parameter activation.
- `model/src/load_ref_files.F` | baseline field/ref-state loading.
- `model/src/load_grid_spacing.F` | grid spacing and metric load behavior.
- `model/src/load_fields_driver.F` | staged model field loading.
- `model/src/external_fields_load.F` | external forcing-field ingestion.
- `pkg/exf/exf_readparms.F` | EXF configuration parser.
- `pkg/exf/exf_init_fixed.F` | EXF fixed initialization state.
- `pkg/bulk_force/bulkf_readparms.F` | bulk forcing settings parser.
- `pkg/bulk_force/bulkf_fields_load.F` | bulk forcing file loading.
- `pkg/obcs/obcs_readparms.F` | open-boundary setup parser.
- `pkg/obcs/obcs_exf_load.F` | OBCS + EXF coupled loading path.
- `pkg/obcs/obcs_fields_load.F` | open-boundary field ingestion.
- `pkg/seaice/seaice_readparms.F` | sea-ice setup parser.
- `pkg/seaice/seaice_model.F` | sea-ice model-step integration.
- `pkg/ptracers/ptracers_readparms.F` | tracer package setup parser.

## Function-level behavior checks
- Confirm each enabled package reaches its `*_READPARMS` routine during startup.
- For forcing mismatches, inspect `*_FIELDS_LOAD` routines and compare expected filenames with `data.*` entries.
- For coupled OBCS/EXF setups, trace `OBCS_EXF_LOAD` inputs and verify boundary interpolation assumptions.
