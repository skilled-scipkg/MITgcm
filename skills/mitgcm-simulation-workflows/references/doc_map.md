# MITgcm documentation map: Simulation Workflows

Generated from documentation roots:
- `doc`
- `verification`
- `doc/examples`
- `tools/example_scripts`
- `utils/python/MITgcmutils/MITgcmutils/examples`

Use this map to stage baseline run, checkpoint, and restart workflows.

## Priority startup docs
- `doc/getting_started/getting_started.rst` | run directory conventions and execution patterns.
- `doc/algorithm/crank-nicol.rst` | timestep-control context for run workflows.
- `verification/tutorial_barotropic_gyre/README.md` | simple forward workflow with reference output.
- `verification/tutorial_baroclinic_gyre/README.md` | multi-stage tutorial workflow with validation points.
- `verification/front_relax/README.md` | variant-input overlays and run sequencing.
- `verification/offline_exf_seaice/README` | offline + coupled workflow patterns.
- `verification/1D_ocean_ice_column/README_11K_TIME_STEP_SIMULATION.TXT` | long-integration operational notes.

## Validation-oriented references
- `verification/tutorial_barotropic_gyre/results/output.txt` | baseline forward-run comparison target.
- `verification/front_relax/results/output.txt` | reference for multi-setup run validation.
- `verification/offline_exf_seaice/results/output.txt` | offline workflow output checkpoint.
