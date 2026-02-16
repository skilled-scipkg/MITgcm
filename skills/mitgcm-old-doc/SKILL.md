---
name: mitgcm-old-doc
description: This skill should be used when users ask about old doc in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Old Doc

## High-Signal Playbook

### Route conditions
- Use this skill when users ask for legacy option names, historical diagnostics behavior, or old open-boundary documentation context.
- Route modern setup/build/run questions to the corresponding core skills (`mitgcm-getting-started`, `mitgcm-build-and-install`, `mitgcm-inputs-and-modeling`).

### Triage questions
- Is the request about legacy diagnostics naming, legacy open-boundary options, or old build notes?
- Which old document is cited (`diags_changes.txt`, `OpenBound.txt`, `optfiles_changes.txt`)?
- Does the user need exact backward mapping to current parameter or routine names?

### Canonical workflow
1. Read the relevant old-doc note for historical context and naming.
2. Map legacy term to current runtime option or source routine.
3. Validate mapping against a modern verification case output/namelist.
4. Report both legacy term and current equivalent path/file.

### Minimal working example
```bash
rg -n "OBCS|open boundary|Sponge" doc/old_doc/OpenBound.txt pkg/obcs
rg -n "diag|diagnostics|DIAG" doc/old_doc/diags_changes.txt pkg/diagnostics model/src
```

### Validation checkpoints
- Legacy option names are linked to currently existing source routines/files.
- Mapped behavior is verified against current diagnostics/open-boundary code paths.

## Scope
- Handle questions about documentation grouped under the 'old-doc' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/old_doc/diags_changes.txt`
- `doc/old_doc/OpenBound.txt`
- `doc/old_doc/optfiles_changes.txt`
- `doc/old_doc/README`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `verification`
- `doc/examples`
- `tools/example_scripts`
- `utils/python/MITgcmutils/MITgcmutils/examples`

## Test references
- `verification`

## Optional deeper inspection
- `eesupp`
- `lsopt`
- `model`
- `optim`
- `pkg`
- `tools`
- `utils/python/MITgcmutils/MITgcmutils`

## Source entry points for unresolved issues
- `model/src/do_statevars_diags.F`
- `pkg/diagnostics/diagnostics_readparms.F`
- `pkg/diagnostics/diagnostics_setdiag.F`
- `pkg/diagnostics/diagstats_calc.F`
- `pkg/diagnostics/diagstats_output.F`
- `pkg/obcs/obcs_readparms.F`
- `pkg/obcs/obcs_check.F`
- `pkg/obcs/obcs_apply_ts.F`
- `pkg/obcs/obcs_apply_uv.F`
- `pkg/obcs/obcs_fields_load.F`
- `pkg/land/land_do_diags.F`
- `pkg/exf/exf_weight_sfx_diags.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
