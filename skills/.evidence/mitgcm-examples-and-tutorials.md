# Evidence: mitgcm-examples-and-tutorials

## Primary docs
- `doc/phys_pkgs/cal.rst`
- `verification/tutorial_reentrant_channel/results/output.txt`
- `verification/tutorial_held_suarez_cs/results/output.txt`
- `doc/phys_pkgs/aim.rst`
- `verification/tutorial_deep_convection/results/output.txt`
- `verification/tutorial_deep_convection/results/output.smag3d.txt`
- `verification/tutorial_baroclinic_gyre/results/output.txt`
- `verification/tutorial_advection_in_gyre/results/output.txt`
- `verification/cfc_example/results/output.txt`
- `doc/phys_pkgs/zonal_filt.rst`
- `doc/phys_pkgs/opps.rst`
- `doc/phys_pkgs/ggl90.rst`

## Primary source entry points
- `skills/mitgcm-examples-and-tutorials/references/doc_map.md`
- `pkg/ptracers/ptracers_zonal_filt_apply.F`
- `pkg/zonal_filt/zonal_filter.F`
- `pkg/zonal_filt/zonal_filt_readparms.F`
- `pkg/zonal_filt/zonal_filt_presmooth.F`
- `pkg/zonal_filt/zonal_filt_postsmooth.F`
- `pkg/zonal_filt/ZONAL_FILT_OPTIONS.h`
- `pkg/zonal_filt/zonal_filt_nofill.F`
- `pkg/zonal_filt/zonal_filt_init.F`
- `pkg/zonal_filt/zonal_filt_apply_uv.F`
- `pkg/zonal_filt/zonal_filt_apply_ts.F`
- `pkg/zonal_filt/ZONAL_FILT.h`
- `pkg/zonal_filt/FFTPACK.h`
- `pkg/zonal_filt/fftpack.F`
- `pkg/tapenade/stubs_tap_tlm.F`
- `pkg/tapenade/stubs_tap_adj.F`
- `pkg/tapenade/COST_TAP_TLM.h`
- `pkg/shap_filt/shap_filt_tracer_s4.F`
- `pkg/shap_filt/shap_filt_tracer_s2.F`
- `pkg/shap_filt/shap_filt_tracer_s1.F`

## Extracted headings
- (none extracted)

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- c      o  cal_PrintError    - Print error messages according to the flags
- (PID.TID 0000.0001) cg2dChkResFreq =   /* 2d con. grad convergence test frequency */
