# Evidence: mitgcm-build-and-install

## Primary docs
- `verification/tutorial_cfc_offline/README.md`
- `verification/natl_box/README.md`
- `verification/tutorial_baroclinic_gyre/README.md`
- `verification/tutorial_reentrant_channel/README.md`
- `verification/tutorial_barotropic_gyre/README.md`
- `verification/flt_example/README.md`
- `doc/autodiff/autodiff.rst`
- `doc/examples/reentrant_channel/reentrant_channel.rst`
- `doc/examples/barotropic_gyre/barotropic_gyre.rst`
- `doc/examples/baroclinic_gyre/baroclinic_gyre.rst`
- `doc/old_doc/optfiles_changes.txt`

## Primary source entry points
- `skills/mitgcm-build-and-install/references/doc_map.md`
- `lsopt/Makefile`
- `pkg/regrid/Makefile`
- `pkg/mnc/Makefile`
- `pkg/exch2/Makefile`
- `eesupp/src/Makefile`
- `tools/cyrus-imapd-makedepend/configure`
- `tools/mpack-1.6/Makefile.in`
- `tools/mpack-1.6/Makefile.am`
- `tools/mpack-1.6/configure`
- `tools/cyrus-imapd-makedepend/Makefile.in`
- `eesupp/inc/DEF_IN_MAKEFILE.h`
- `pkg/offline/offline_fields_load.F`
- `pkg/flt/flt_main.F`
- `pkg/cfc/cfc_fields_load.F`
- `pkg/autodiff/autodiff_ini_model_io.F`
- `pkg/profiles/profiles_make_ncfile.F`
- `pkg/offline/OFFLINE_SWITCH.h`
- `pkg/offline/offline_reset_parms.F`
- `pkg/offline/offline_readparms.F`

## Extracted headings
- include ``checkpoint_lev3.h''
- include ``checkpoint_lev2.h''
- include ``checkpoint_lev1.h''
- Assuming $PWD is the build subdirectory
- Clean stuff
- Use your own optfile
- Differentiate code to generate TLM code using Tapenade
- Creates executable mitgcmuv_tap_tlm
- Rest of the setup is standard
- Differentiate code to generate adjoint code using Tapenade

## Executable command hints
- ./prepare_run
- ./mitgcmuv > output.txt
- ./mitgcmuv_tap_tlm > output_tap_tlm.txt 2>&1
- ./mitgcmuv_tap_adj > output_tap_adj.txt 2>&1

## Warnings and pitfalls
- nevertheless are important to the aspect of *tangent* linearity; note
- We note an important aspect of the forward vs. reverse mode calculation.
- - Two important issues related to the handling of the control
- an important difference: Since the boundary values are time
- **WARNING:** If the structure of the common blocks :varlink:`dynvars_r`,
- Although important aspects of the of the Southern Ocean and Antarctic Circumpolar Current
- (using the MITgcm) with some important differences,
- of solution fidelity and stability. Although our topography is idealized, the topography is
- with an important difference: we use a high-order
- Numerical Stability Criteria
- We now examine numerical stability criteria to help choose and assess parameters for our coarse resolution study:
- CFL condition :eq:`eq_SOch_cfl_stability` and the stability of inertial oscillations :eq:`eq_SOCh_inertial_stability`:
