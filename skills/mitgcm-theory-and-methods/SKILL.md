---
name: mitgcm-theory-and-methods
description: This skill should be used when users ask about theory and methods in MITgcm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# MITgcm: Theory and Methods

## High-Signal Playbook

### Route conditions
- Use this skill for discretization, advection/time-stepping selection, free-surface formulation, and grid-method questions (docs: `doc/algorithm/algorithm.rst`, `doc/algorithm/adv-schemes.rst`, `doc/algorithm/nonlinear-freesurf.rst`).
- Route experiment execution/build mechanics to `mitgcm-build-and-install`.
- Route package-specific forcing/input wiring to `mitgcm-inputs-and-modeling`.
- Route result-log interpretation and run-to-run comparison to `mitgcm-analysis-and-output`.

### Triage questions
- Hydrostatic or non-hydrostatic target dynamics?
- Linear or non-linear free surface (`nonlinFreeSurf` path) and is strict tracer conservation required?
- Which tracer/momentum advection scheme code is intended (`tempAdvScheme`, etc.)?
- AB-II or AB-III time stepping, and are forcing/dissipation terms kept in AB extrapolation?
- Grid type (Cartesian, spherical, curvilinear) and whether partial cells are active?
- Expected maximum velocity/Coriolis scales for CFL and inertial-stability checks?

### Canonical workflow
1. Choose pressure/free-surface formulation (rigid lid, implicit linear FS, or nonlinear FS) from algorithm docs.
2. Set time stepping: AB-II default or AB-III (`ALLOW_ADAMSBASHFORTH_3`) with documented `alpha_AB`, `beta_AB` behavior.
3. Select advection scheme by code and ensure overlap (`OLx/OLy`) is sufficient for the stencil (docs: `doc/algorithm/adv-schemes.rst`).
4. Configure horizontal/vertical grid descriptors and partial-cell settings (docs: `doc/algorithm/horiz-grid.rst`, `doc/algorithm/vert-grid.rst`).
5. Run a short integration and inspect stability indicators (`cg2d`, monitor output, extrema behavior).
6. Adjust timestep/dissipation and repeat until CFL and residual behavior are within documented stable ranges.

### Minimal working example
```fortran
# parameter choices pattern (data + CPP options)
#define ALLOW_ADAMSBASHFORTH_3

&PARM03
 momDissip_In_AB = .FALSE.,
/

&PARM01
 nonlinFreeSurf = 4,
/

# advection codes are set in input/data, e.g. tempAdvScheme=3
```

### Pitfalls and fixes
- AB-II with too small stabilization (`epsilon_AB`) can be weakly unstable for oscillatory terms; use documented stabilized settings (docs: `doc/algorithm/algorithm.rst`).
- AB-III improves oscillatory CFL (~0.72; up to ~0.786 with altered coefficients) but reduces damping-problem stability (~0.54); move dissipation outside AB when needed (docs: `doc/algorithm/algorithm.rst`).
- Centered 2nd/4th-order advection without adequate diffusion is noisy (docs: `doc/algorithm/adv-schemes.rst`).
- Large-stencil schemes without enough overlap (`OLx/OLy`) create boundary/halo issues; account for cubed-sphere wet-corner cost (docs: `doc/algorithm/adv-schemes.rst`).
- Linear free-surface can lose tracer-content consistency for large surface variation; prefer `nonlinFreeSurf=4` for full form (docs: `doc/algorithm/nonlinear-freesurf.rst`).
- Partial-cell/topography choices that leave overly thin cells can destabilize flow; verify vertical-grid and hFac settings (docs: `doc/algorithm/vert-grid.rst`).

### Convergence and validation checks
- Compute and monitor advective and inertial stability metrics against documented tutorial criteria (docs: `doc/examples/barotropic_gyre/barotropic_gyre.rst`, `doc/examples/reentrant_channel/reentrant_channel.rst`).
- Confirm `cg2d_last_res` and iteration counts remain below configured tolerances across multiple steps.
- For advection-scheme studies, verify expected diffusion/dispersion/positivity behavior against reference scheme summaries.
- For nonlinear free surface, check for negligible global tracer drift in long tests when exact conservation pathway is enabled.
- Perform one grid/timestep refinement check; key diagnostics should trend consistently.

## Scope
- Handle questions about theoretical background and algorithmic methods.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/algorithm/nonlinear-freesurf.rst`
- `doc/algorithm/algorithm.rst`
- `doc/algorithm/adv-schemes.rst`
- `doc/algorithm/horiz-grid.rst`
- `doc/algorithm/vert-grid.rst`
- `doc/algorithm/c-grid.rst`
- `doc/algorithm/finitevol-meth.rst`

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
- `model/src/solve_for_pressure.F`
- `model/src/timestep.F`
- `model/src/correction_step.F`
- `model/src/ini_vertical_grid.F`
- `pkg/generic_advdiff/gad_c2_adv_x.F`
- `pkg/generic_advdiff/gad_u3_adv_x.F`
- `pkg/generic_advdiff/gad_fluxlimit_adv_x.F`
- `pkg/mom_fluxform/mom_u_adv_uu.F`
- `pkg/mom_fluxform/mom_v_adv_vv.F`
- `pkg/obcs/OBCS_GRID.h`
- `pkg/streamice/STREAMICE_ADV.h`
- `pkg/gridalt/make_phys_grid.F`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" eesupp lsopt model optim pkg tools utils/python/MITgcmutils/MITgcmutils`).
