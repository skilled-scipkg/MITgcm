# Evidence: mitgcm-inputs-and-modeling

## Primary docs
- `verification/global_with_exf/README.md`
- `verification/seaice_obcs/README.md`
- `verification/global_oce_biogeo_bling/input_ad/README.txt`
- `doc/old_doc/notes_c37_adj.txt`
- `doc/software_arch/software_arch.rst`
- `doc/related_projects/related_projects.rst`
- `doc/phys_pkgs/bulk_force.rst`
- `doc/ocean_state_est/ocean_state_est.rst`
- `doc/examples/rotating_tank/rotating_tank.rst`
- `doc/examples/plume_on_slope/plume_on_slope.rst`
- `verification/fizhi-cs-32x32x40/results/output.txt`
- `doc/examples/examples.rst`

## Primary source entry points
- `skills/mitgcm-inputs-and-modeling/references/doc_map.md`
- `pkg/seaice/seaice_obcs_output.F`
- `model/src/do_oceanic_phys.F`
- `pkg/bulk_force/bulkf_fields_load.F`
- `pkg/seaice/seaice_ocean_stress.F`
- `pkg/seaice/seaice_budget_ocean.F`
- `pkg/fizhi/update_ocean_exports.F`
- `pkg/fizhi/fizhi_ocean_coms.h`
- `pkg/bulk_force/bulkf_flux_adjust.F`
- `pkg/seaice/seaice_model.F`
- `pkg/seaice/seaice_tracer_phys.F`
- `pkg/seaice/seaice_output.F`
- `pkg/seaice/seaice_diagnostics_state.F`
- `pkg/seaice/seaice_check_pickup.F`
- `pkg/seaice/seaice_check.F`
- `pkg/seaice/seaice_ad_check_lev4_dir.h`
- `pkg/seaice/seaice_ad_check_lev3_dir.h`
- `pkg/seaice/seaice_ad_check_lev2_dir.h`
- `pkg/seaice/seaice_ad_check_lev1_dir.h`
- `pkg/seaice/advect.F`

## Extracted headings
- Example "eedata" file
- Lines beginning "#" are comments
- nTx - No. threads per process in X
- nTy - No. threads per process in Y
- \*****************\*
- PROFILES cost function
- *********************
- OBSFIT cost function

## Executable command hints
- ./prepare_run
- ./mitgcmuv_ad >& output_adm.txt
- mpirun -np 64 -machinefile mf ./mitgcmuv

## Warnings and pitfalls
- reporting status and configuration information and for reporting error
- then usually an error will be
- We find the “integrated flux profile” for momentum and stability if
- Important Notes
- | :math:`R_i`                       | data error covariance matrix      |
- In the current implementation, model-data error covariance matrices
- Error handling
