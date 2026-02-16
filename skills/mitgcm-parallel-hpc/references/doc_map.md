# MITgcm documentation map: Parallel and HPC

Generated from documentation roots:
- `doc`
- `verification`
- `doc/examples`
- `tools/example_scripts`
- `utils/python/MITgcmutils/MITgcmutils/examples`

Use this map to choose a documented MPI/OpenMP baseline before source-level debugging.

## Priority startup docs
- `doc/getting_started/getting_started.rst` | canonical MPI/OpenMP build/run guidance.
- `doc/phys_pkgs/exch2.rst` | EXCH2 topology and decomposition behavior.
- `verification/lab_sea/README.md` | compact MPI starter workflow with explicit commands.
- `verification/global_ocean.90x40x15/README` | practical multi-rank decomposition examples.
- `verification/global_ocean.cs32x15/README` | cubed-sphere decomposition and runtime checks.
- `verification/cpl_aim+ocn/README.md` | coupled MPI launch workflow.
- `verification/adjustment.cs-32x32x1/README` | EXCH2 + MPI test setup notes.
- `verification/hs94.1x64x5/README` | additional atmospheric MPI baseline case.

## Validation-oriented references
- `verification/lab_sea/results/output.txt` | baseline stdout comparison target.
- `verification/global_ocean.90x40x15/results/output.txt` | decomposition-sensitive output reference.
- `verification/cpl_aim+ocn/results/ocnSTDOUT.0000` | coupled ocean-component reference output.
