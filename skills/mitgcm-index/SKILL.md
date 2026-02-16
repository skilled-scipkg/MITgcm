---
name: mitgcm-index
description: This skill should be used when users ask how to use MITgcm and the correct generated documentation skill must be selected before going deeper into source code.
---

# MITgcm Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.
- Use enriched core skills first for realistic simulation setup/run/validation, then escalate to supporting topics.

## Generated topic skills
- `mitgcm-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `mitgcm-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `mitgcm-inputs-and-modeling`: Inputs and Modeling (inputs, forcing, package setup, and model configuration)
- `mitgcm-theory-and-methods`: Theory and Methods (discretization, advection/time-stepping, free-surface, and grid methods)
- `mitgcm-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorial pathways, and variant comparisons)
- `mitgcm-analysis-and-output`: Analysis and Output (stdout diagnostics, output validation, and post-run checks)
- `mitgcm-parallel-hpc`: Parallel and HPC (MPI/OpenMP/GPU execution, scaling, and batch systems)
- `mitgcm-simulation-workflows`: Simulation Workflows (run/restart/checkpoint execution flow and controls)
- `mitgcm-verification`: Verification (verification framework references and test harness context)
- `mitgcm-old-doc`: Old Doc (legacy notes and historical documentation)
- `mitgcm-advanced-topics`: Advanced Topics (collapsed low-frequency docs: API/scripting, general index, phys-pkgs one-offs, references, requirements, utilities)

## Documentation-first inputs
- `doc`

## Tutorials and examples roots
- `verification`
- `doc/examples`
- `tools/example_scripts`
- `utils/python/MITgcmutils/MITgcmutils/examples`

## Test roots for behavior checks
- `verification`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, search the topic skill `references/doc_map.md`.
- If documentation still leaves ambiguity, open `references/source_map.md` inside the same topic skill and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).

## Source directories for deeper inspection
- `eesupp`
- `lsopt`
- `model`
- `optim`
- `pkg`
- `tools`
- `utils/python/MITgcmutils/MITgcmutils`
