# Evidence: mitgcm-theory-and-methods

## Primary docs
- `doc/algorithm/nonlinear-freesurf.rst`
- `doc/algorithm/algorithm.rst`
- `doc/algorithm/adv-schemes.rst`
- `doc/algorithm/horiz-grid.rst`
- `doc/algorithm/vert-grid.rst`
- `doc/algorithm/c-grid.rst`
- `doc/algorithm/finitevol-meth.rst`

## Primary source entry points
- `skills/mitgcm-theory-and-methods/references/doc_map.md`
- `model/src/ini_vertical_grid.F`
- `pkg/streamice/streamice_adv_front.F`
- `pkg/streamice/streamice_adv_flux_fl_y.F`
- `pkg/streamice/streamice_adv_flux_fl_x.F`
- `pkg/streamice/STREAMICE_ADV.h`
- `pkg/obcs/obcs_u1_adv_tracer.F`
- `pkg/obcs/OBCS_GRID.h`
- `pkg/mom_fluxform/mom_v_adv_wv.F`
- `pkg/mom_fluxform/mom_v_adv_vv.F`
- `pkg/mom_fluxform/mom_v_adv_uv.F`
- `pkg/mom_fluxform/mom_u_adv_wu.F`
- `pkg/mom_fluxform/mom_u_adv_vu.F`
- `pkg/mom_fluxform/mom_u_adv_uu.F`
- `pkg/mnc/mnc_grid.F`
- `pkg/mnc/mnc_cw_write_grid_info.F`
- `pkg/matrix/matrix_write_grid.F`
- `pkg/gridalt/make_phys_grid.F`
- `pkg/generic_advdiff/gad_u3_adv_y.F`
- `pkg/generic_advdiff/gad_u3_adv_x.F`

## Extracted headings
- (none extracted)

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- -  when the solver does not iterate until convergence; for example,
- corresponds to a reduced stability compared to a simple forward
- A stability analysis for an oscillation equation should be given at this
- A stability analysis for a relaxation equation should be given at this
- stability limit for an oscillatory problem like advection or Coriolis.
- stability limit can be further extended up to a CFL of 0.786 for an
- is less favorable, since the stability limit is reduced to 0.54 only
- second order accuracy and more stability.
- numerical stability; alternative definitions break the conservation
- scale parameter :math:`L_{\rm Shap}`. The stability of this S2g filter
- caution, however, since it effectively implies that viscous terms are
- model stability is not usually as sensitive to vertical viscosity.
