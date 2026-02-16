# Evidence: mitgcm-getting-started

## Primary docs
- `verification/front_relax/README.md`
- `verification/global_ocean_ebm/README.md`
- `verification/lab_sea/README.md`
- `verification/global_oce_latlon/README.md`
- `verification/tutorial_plume_on_slope/README.md`
- `verification/solid-body.cs-32x32x1/README.md`
- `doc/overview/overview.rst`
- `verification/exp4/README.md`
- `verification/atm_gray/README.md`
- `verification/cpl_aim+ocn/README.md`
- `doc/phys_pkgs/ptracers.rst`
- `doc/phys_pkgs/phys_pkgs.rst`

## Primary source entry points
- `skills/mitgcm-getting-started/references/doc_map.md`
- `pkg/atm_ocn_coupler/cpl_send_ocn_fields.F`
- `pkg/atm_ocn_coupler/cpl_send_atm_fields.F`
- `pkg/atm_ocn_coupler/cpl_recv_ocn_fields.F`
- `pkg/atm_ocn_coupler/cpl_recv_atm_fields.F`
- `pkg/atm_ocn_coupler/cpl_send_ocn_cplparms.F`
- `pkg/atm_ocn_coupler/cpl_send_ocn_atmconfig.F`
- `pkg/atm_ocn_coupler/cpl_send_atm_ocnconfig.F`
- `pkg/atm_ocn_coupler/cpl_send_atm_cplparms.F`
- `pkg/atm_ocn_coupler/cpl_register_ocn.F`
- `pkg/atm_ocn_coupler/cpl_register_atm.F`
- `pkg/atm_ocn_coupler/cpl_recv_ocn_ocnconfig.F`
- `pkg/atm_ocn_coupler/cpl_recv_atm_atmconfig.F`
- `pkg/atm_ocn_coupler/cpl_read_params.F`
- `pkg/atm_ocn_coupler/CPL_PARAMS.h`
- `pkg/atm_ocn_coupler/CPL_MAP2GRIDS.h`
- `pkg/atm_ocn_coupler/cpl_init_ocn_vars.F`
- `pkg/atm_ocn_coupler/cpl_init_atm_vars.F`
- `pkg/atm_ocn_coupler/cpl_check_cplconfig.F`
- `pkg/seaice/seaice_ocean_stress.F`

## Extracted headings
- Relaxation of a front in a channel : simplest example that uses GM-Redi parameterization
- Overview:
- Instructions:
- Notes:
- Global Ocean Simulation at 4 degree Resolution, Alternative Forcing
- Instructions for Forward tests:
- Instructions for Adjoint tests:
- Primary test Overview:
- Lab Sea adjoint
- Instructions
- 1-CPU forward experiment
- 2-CPU forward experiment

## Executable command hints
- $N = 2\times 10^{-3} ~s^{-1}$, see matlab script `input/gendata.m`),
- ./prepare_run          #- only for "bvp" test
- $1.4\times 10^{-4}$, $2.3 \times 10^{-5}$ and RMS: $6.6 \times 10^{-5}$,
- $9.6 \times 10^{-6}$ ) come from the dynamics and not from GM since without
- ./mitgcmuv > output.txt
- mpirun -np 2 ../build/mitgcmuv
- ./do_run.sh
- ./testreport -t lab_sea [-of my_platform_optionFile]
- ./testreport -t lab_sea -ad [-of my_platform_optionFile]
- ./prepare_run
- $$ U(\phi) = U_{eq} ~ \cos( \phi ) ~~~ \mathrm{with:} ~~~ U_{eq} = \omega' \times R $$
- $$ \eta(\phi) = \rho_{const} ~ U_{eq} ~ ( \Omega R + U_{eq} / 2 ) ~~ ( \cos^{2}(\phi) - 2/3 ) $$

## Warnings and pitfalls
- (none extracted)
