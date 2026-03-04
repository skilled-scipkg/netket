---
name: netket-user-guides
description: This skill should be used when users ask about user guides in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: User Guides

## High-Signal Playbook
### Route conditions
- Route to `netket-inputs-and-modeling` for concrete object construction choices.
- Route to `netket-simulation-workflows` for run-loop execution and checkpoint policy.
- Route to `netket-api-and-scripting` for strict API signature/module lookup.

### Triage questions
- Is the user asking conceptual guidance (why) or API mechanics (how)?
- Are they focused on SR/QGT behavior or operator/module semantics?
- Are they following modern `VMC_SR` guidance or older SR-style snippets?
- Do they need module-level deep guide (`hilbert`, `operator`, `sampler`, `drivers`, `sr`, `utils`)?
- Are numerical stability issues (small QGT eigenvalues/regularization) the main blocker?

### Canonical workflow
1. Start from `docs/user-guides/index-modules.md` to choose the right deep guide.
2. For optimization geometry questions, use `docs/user-guides/sr.md` plus `docs/api/optimizer.md`.
3. For operator behavior, use `docs/user-guides/operator.md` and operator API pages.
4. For runtime module interactions, use `drivers.md`, `varstate.md`, and sampler guide.
5. Translate conceptual advice into one actionable config (`diag_shift`, sampler setting, callback, etc.).
6. Cross-link one adjacent skill if the request shifts to implementation details.

### Minimal working example
```python
import optax
import netket as nk

# SR schedule from user guide patterns
sr = nk.optimizer.SR(diag_shift=optax.linear_schedule(0.01, 0.0001, 100))

# Equivalent modern path: use VMC_SR directly with diag_shift
# driver = nk.driver.VMC_SR(H, opt, variational_state=vs, diag_shift=0.01)
```

### Pitfalls and fixes
- `docs/user-guides/sr.md` mixes historical and modern guidance; prefer `VMC_SR` for new workflows. (`docs/user-guides/sr.md`, `docs/api/drivers.md`)
- Ill-conditioned QGT can destabilize updates; use `diag_shift`/schedules and suitable solver. (`docs/user-guides/sr.md`, `docs/api/optimizer.md`)
- Constraints + local sampler mismatch can break intended invariant subspace exploration. (`docs/user-guides/hilbert.md`)
- Confusing module maps: start from index-modules to avoid jumping across unrelated docs. (`docs/user-guides/index-modules.md`)
- Utility modules under `netket.utils` are not all stability-guaranteed unless explicitly documented in API. (`docs/api/api-stability.md`)

### Convergence and validation checks
- SR regularization is explicit and not left to accidental defaults.
- Loss/energy variance and acceptance move in the expected direction over early iterations.
- Driver/logger outputs include the quantities implied by the chosen guide.
- Chosen guidance aligns with public API stability constraints.

## Scope
- Handle questions about documentation grouped under the `user-guides` theme.
- Emphasize conceptual correctness and recommended modern defaults.

## Primary documentation references
- `docs/user-guides/index-modules.md`
- `docs/user-guides/sr.md`
- `docs/user-guides/drivers.md`
- `docs/user-guides/varstate.md`
- `docs/user-guides/operator.md`
- `docs/user-guides/hilbert.md`
- `docs/user-guides/sampler.ipynb`
- `docs/user-guides/utils/index.md`

## Workflow
- Start from module index to pick one focused guide.
- Use API pages only to confirm signatures/availability.
- If unresolved, consult `references/doc_map.md` and then `references/source_map.md`.
- Cite exact docs file paths in responses.

## Tutorials and examples
- `docs/tutorials`
- `Examples`

## Test references
- `test/driver`
- `test/sampler`
- `test/operator`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/optimizer/sr.py` (SR preconditioner configuration and schedules)
- `netket/optimizer/qgt/default.py` (QGT backend auto-selection)
- `netket/optimizer/solver/solvers.py` (solver behavior and diagnostics)
- `netket/driver/vmc.py` and `netket/_src/driver/vmc_sr.py` (legacy vs modern SR run flow)
- `netket/operator/__init__.py` and `netket/operator/_fermion2nd/utils.py` (operator module edges)
- `netket/utils/__init__.py` (utility-module entry surface)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
