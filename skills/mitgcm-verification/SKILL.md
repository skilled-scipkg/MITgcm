---
name: mitgcm-verification
description: This skill should be used when users ask about verification in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Verification

## High-Signal Playbook

### Route conditions
- Use this skill for regression workflow design, `verification/testreport` usage, and pass/fail interpretation.
- Route case physics/input design to `mitgcm-inputs-and-modeling`.
- Route build-toolchain failures to `mitgcm-build-and-install`.
- Route output diagnostics deep dive to `mitgcm-analysis-and-output`.

### Triage questions
- Is this a single-case check or a multi-case regression sweep?
- Forward-only, adjoint, TLM, or Tapenade/OpenAD mode?
- Serial or MPI verification run?
- Which comparison strictness is needed (`-match` digits, tolerance expectations)?
- Is failure from build stage, run stage, or output-comparison stage?

### Canonical workflow
1. Pick one verification case and get a passing baseline before broad test batches.
2. Use `verification/testreport` for reproducible build/run/compare workflow.
3. Keep run mode explicit (`-mpi`, `-ad`, `-tlm`, `-tap`) and choose matching references.
4. Inspect generated output logs and similarity reports before changing physics options.
5. Expand to grouped tests only after single-case baseline is stable.

### Minimal working example
```bash
cd verification
./testreport -t tutorial_barotropic_gyre -match 8
```
```bash
# MPI variant smoke test
cd verification
./testreport -t lab_sea -mpi -match 8
```

### Pitfalls and fixes
- Running large verification sets before single-case baseline obscures first failure root cause.
- Mismatch between run mode and reference outputs (serial vs MPI, AD vs forward) yields false failures.
- Overly strict matching without accounting for documented tolerance differences triggers noisy regressions.
- Treating comparison failure as physics bug before confirming build flags and runtime mode.

### Convergence and validation checks
- `testreport` summary should clearly separate build, run, and comparison results.
- For each case, final `Iter.Nb` and key monitor diagnostics should align with reference expectations.
- Similarity metrics should meet requested matching criteria for the selected run mode.
- Re-run failing case in isolation before changing shared configuration.

## Scope
- Handle questions about verification framework references and test harness context.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `verification/README.md`
- `verification/testreport`
- `doc/examples/examples.rst`
- `verification/tutorial_barotropic_gyre/README.md`
- `verification/front_relax/README.md`
- `verification/lab_sea/README.md`
- `verification/isomip/code_tap/README_TAP_HACKS.txt`

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
- `verification/testreport`
- `verification/verification_parser.py`
- `tools/genmake2`
- `tools/do_tst_2+2`
- `model/src/config_summary.F`
- `model/src/do_statevars_diags.F`
- `pkg/autodiff/autodiff_ini_model_io.F`
- `pkg/autodiff/autodiff_store.F`
- `pkg/autodiff/autodiff_restore.F`
- `pkg/tapenade/stubs_tap_tlm.F`
- `pkg/tapenade/stubs_tap_adj.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
