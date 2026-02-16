---
name: mitgcm-advanced-topics
description: This skill should be used for advanced or low-frequency MITgcm topics collapsed from one-doc themes; it prioritizes documentation references and then targeted source inspection.
---

# MITgcm: Advanced Topics

## Scope
- Handle lower-frequency topics collapsed from single-doc skills: API/scripting edge cases, general manual index, standalone references/requirements docs, utilities overview, and THSICE one-off package detail.
- Keep responses docs-first and concise; route common simulation questions back to enriched core skills.

## Route the request
- Route common setup/build/modeling/run/output requests to core skills first:
  - `mitgcm-getting-started`
  - `mitgcm-build-and-install`
  - `mitgcm-inputs-and-modeling`
  - `mitgcm-theory-and-methods`
  - `mitgcm-examples-and-tutorials`
  - `mitgcm-analysis-and-output`
- Use this skill when the user explicitly asks for one of these niche areas:
  - `doc/phys_pkgs/shap_filt.rst`
  - `doc/index.rst`
  - `doc/phys_pkgs/thsice.rst`
  - `doc/references.rst`
  - `doc/requirements.txt`
  - `doc/utilities/utilities.rst`

## Primary documentation references
- `doc/phys_pkgs/shap_filt.rst`
- `doc/index.rst`
- `doc/phys_pkgs/thsice.rst`
- `doc/references.rst`
- `doc/requirements.txt`
- `doc/utilities/utilities.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the full combined inventory.
- If implementation behavior is still unclear, inspect `references/source_map.md` for targeted entry points.
- Cite exact documentation file paths in responses.

## Source entry points for unresolved issues
- `pkg/shap_filt/shap_filt_readparms.F`
- `pkg/shap_filt/shap_filt_apply_ts.F`
- `pkg/shap_filt/shap_filt_apply_uv.F`
- `pkg/thsice/thsice_main.F`
- `pkg/thsice/THSICE_PARAMS.h`
- `pkg/thsice/thsice_readparms.F`
- `pkg/thsice/thsice_output.F`
- `utils/python/MITgcmutils/MITgcmutils/mds.py`
- `utils/python/MITgcmutils/MITgcmutils/mnc.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
