# MITgcm source map: Advanced Topics

Use this map after the topic docs in `references/doc_map.md` and only when behavior is unclear.

## Fast source navigation
- `rg -n "<symbol_or_keyword>" pkg utils/python/MITgcmutils/MITgcmutils optim`
- `rg -n "SUBROUTINE|FUNCTION|def " pkg/shap_filt pkg/thsice utils/python/MITgcmutils/MITgcmutils`

## Suggested source entry points
- `pkg/shap_filt/shap_filt_readparms.F` | parse SHAP_FILT runtime options.
- `pkg/shap_filt/shap_filt_apply_ts.F` | apply SHAP_FILT to tracer fields.
- `pkg/shap_filt/shap_filt_apply_uv.F` | apply SHAP_FILT to velocity fields.
- `pkg/thsice/thsice_readparms.F` | ingest THSICE runtime configuration.
- `pkg/thsice/thsice_main.F` | THSICE package driver for each step.
- `pkg/thsice/thsice_output.F` | THSICE diagnostics and output writes.
- `pkg/thsice/THSICE_PARAMS.h` | key THSICE control parameters.
- `utils/python/MITgcmutils/MITgcmutils/mds.py` | MDS binary read/write helpers used in analysis scripts.
- `utils/python/MITgcmutils/MITgcmutils/mnc.py` | NetCDF (MNC) helpers for post-processing pipelines.
- `optim/optim_main.F` | optimization driver context for advanced estimation workflows.

## Function-level behavior checks
- Confirm `SHAP_FILT_READPARMS` sets expected switches before `SHAP_FILT_APPLY_TS`/`SHAP_FILT_APPLY_UV` calls.
- Confirm `THSICE_READPARMS` populates values consumed in `THSICE_MAIN` and `THSICE_OUTPUT`.
- For Python tooling, trace `rdmds`/`wrmds` behavior in `mds.py` and compare metadata assumptions with target files.
