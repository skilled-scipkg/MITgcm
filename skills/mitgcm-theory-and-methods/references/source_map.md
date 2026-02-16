# MITgcm source map: Theory and Methods

Use this map after docs in `references/doc_map.md` for algorithmic details and discretization behavior.

## Fast source navigation
- `rg -n "adams|cg2d|pressure|adv|grid|correction_step|freeSurf" model/src pkg/generic_advdiff pkg/mom_fluxform pkg/gridalt pkg/obcs`
- `rg -n "SUBROUTINE (TIMESTEP|ADAMS_BASHFORTH|SOLVE_FOR_PRESSURE|GAD_|MOM_)" model/src pkg/generic_advdiff pkg/mom_fluxform`

## Suggested source entry points
- `model/src/dynamics.F` | core dynamics sequencing.
- `model/src/timestep.F` | timestep-level algorithm application.
- `model/src/adams_bashforth2.F` | AB-II implementation details.
- `model/src/adams_bashforth3.F` | AB-III implementation details.
- `model/src/solve_for_pressure.F` | pressure-solver coupling logic.
- `model/src/correction_step.F` | predictor/corrector coupling.
- `model/src/cg2d.F` | barotropic solve iteration behavior.
- `model/src/ini_vertical_grid.F` | vertical grid/discretization setup.
- `model/src/ini_grid.F` | global grid setup.
- `pkg/generic_advdiff/gad_c2_adv_x.F` | centered second-order tracer advection.
- `pkg/generic_advdiff/gad_u3_adv_x.F` | third-order upwind tracer advection.
- `pkg/generic_advdiff/gad_fluxlimit_adv_x.F` | flux-limiter advection behavior.
- `pkg/generic_advdiff/gad_ppm_adv_x.F` | PPM advection behavior.
- `pkg/mom_fluxform/mom_u_adv_uu.F` | momentum advection in U equation.
- `pkg/mom_fluxform/mom_v_adv_vv.F` | momentum advection in V equation.
- `pkg/gridalt/make_phys_grid.F` | alternate-grid generation logic.
- `pkg/obcs/OBCS_GRID.h` | boundary-grid coupling constants.

## Function-level behavior checks
- Validate AB choices by comparing calls into `ADAMS_BASHFORTH2`/`ADAMS_BASHFORTH3` from `TIMESTEP`.
- For pressure issues, inspect `SOLVE_FOR_PRESSURE` and `CG2D` residual evolution together.
- For tracer differences, compare selected `GAD_*` routine path with configured advection scheme code.
