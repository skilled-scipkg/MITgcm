# Evidence: mitgcm-analysis-and-output

## Primary docs
- `verification/ideal_2D_oce/results/output.txt`
- `verification/global_ocean.90x40x15/results/output.txt`
- `verification/global_ocean.90x40x15/results/output.dwnslp.txt`
- `verification/fizhi-cs-aqualev20/results/output.txt`
- `verification/atm_gray/results/output.txt`
- `verification/global_ocean.cs32x15/results/output.in_p.txt`
- `verification/global_ocean.cs32x15/results/output.thsice.txt`
- `verification/atm_gray/results/output.ape.txt`
- `verification/aim.5l_cs/results/output.thSI.txt`
- `verification/vermix/results/output.gglLC.txt`
- `verification/vermix/results/output.ggl90.txt`
- `verification/shelfice_2d_remesh/results/output.txt`

## Primary source entry points
- `skills/mitgcm-analysis-and-output/references/doc_map.md`
- `pkg/thsice/thsice_slab_ocean.F`
- `pkg/thsice/thsice_get_ocean.F`
- `pkg/seaice/seaice_ocean_stress.F`
- `pkg/seaice/seaice_map_thsice.F`
- `pkg/seaice/seaice_budget_ocean.F`
- `pkg/thsice/thsice_output.F`
- `pkg/shelfice/shelfice_mask_seaice.F`
- `pkg/seaice/seaice_output.F`
- `pkg/seaice/seaice_obcs_output.F`
- `pkg/fizhi/update_ocean_exports.F`
- `pkg/fizhi/fizhi_ocean_coms.h`
- `pkg/atm_compon_interf/atm_store_thsice.F`
- `pkg/aim_v23/phy_suflux_ocean.F`
- `pkg/seaice/seaice_oceandrag_coeffs.F`
- `pkg/atm2d/sum_thsice_out.F`
- `pkg/atm2d/pass_thsice_fluxes.F`
- `pkg/atm_compon_interf/atm_store_aim_fields.F`
- `pkg/shelfice/shelfice_remesh_uv_mask.F`
- `pkg/shelfice/shelfice_remesh_state.F`

## Extracted headings
- (none extracted)

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- (PID.TID 0000.0001) cg2dChkResFreq =   /* 2d con. grad convergence test frequency */
- (PID.TID 0000.0001) zolmin = /* minimum stability parameter [?] */
- (PID.TID 0000.0001) useStabilityFct_overIce= /* transfert Coeffs over sea-ice depend on stability */
