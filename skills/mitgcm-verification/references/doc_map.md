# MITgcm documentation map: Verification

Generated from documentation roots:
- `doc`
- `verification`
- `doc/examples`
- `tools/example_scripts`
- `utils/python/MITgcmutils/MITgcmutils/examples`

Use this map to choose verification harness docs and case-level references before escalating to source.

## Priority startup docs
- `verification/README.md` | high-level verification experiment entry points.
- `verification/testreport` | end-to-end build/run/compare harness usage and options.
- `doc/examples/examples.rst` | catalog of tutorial/verification experiment objectives.
- `verification/tutorial_barotropic_gyre/README.md` | compact baseline case for first-pass regression checks.
- `verification/front_relax/README.md` | multi-configuration reference case.
- `verification/lab_sea/README.md` | forward + adjoint verification workflow.
- `verification/tutorial_cfc_offline/README.md` | offline verification workflow example.
- `verification/isomip/code_tap/README_TAP_HACKS.txt` | Tapenade-specific verification notes.

## Validation-oriented references
- `verification/tutorial_barotropic_gyre/results/output.txt` | forward reference output.
- `verification/lab_sea/results/output_adm.txt` | adjoint reference output.
- `verification/front_relax/results/output.txt` | core forward regression target.
- `verification/verification_parser.py` | parser script used by verification metadata tooling.
