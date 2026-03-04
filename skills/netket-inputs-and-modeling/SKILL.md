---
name: netket-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Route to `netket-api-and-scripting` for API enumeration or serialization details.
- Route to `netket-simulation-workflows` once the model/system is fixed and the question is about run strategy.
- Route to `netket-user-guides` for SR/QGT conceptual guidance beyond model setup.

### Triage questions
- What Hilbert space is intended (`Spin`, `Fock`, `Qubit`, constrained variants)?
- Is the system discrete, continuous, or mixed/experimental geometry?
- Which operator family is needed (`Ising`, `Heisenberg`, custom operator)?
- Which model framework is used (Flax preferred vs custom framework wrappers)?
- Is sampler choice compatible with Hilbert constraints?
- Is this MC sampling (`MCState`) or exact/full-summation (`FullSumState`)?

### Canonical workflow
1. Define graph/geometry and Hilbert space first (`docs/user-guides/hilbert.md`, `docs/api/geometry.md`).
2. Define the operator on the same Hilbert space (`docs/user-guides/operator.md`).
3. Choose a model API (Flax recommended) and instantiate with explicit dtype (`docs/advanced/custom_models.md`, `docs/api/models.md`).
4. Choose a sampler compatible with constraints (`docs/user-guides/hilbert.md`, `docs/user-guides/sampler.ipynb`).
5. Construct `MCState` or `FullSumState` and check `n_samples`, `n_discard_per_chain`, chunking as needed (`docs/user-guides/varstate.md`).
6. Validate shapes/parameter tree before long runs.
7. Escalate to model/sampler source only if docs do not explain behavior.

### Minimal working example
```python
import netket as nk

L = 20
g = nk.graph.Chain(length=L, pbc=True)
hi = nk.hilbert.Spin(s=1 / 2, N=g.n_nodes, total_sz=0)
ha = nk.operator.Heisenberg(hilbert=hi, graph=g)

ma = nk.models.RBMSymm(symmetries=g.translation_group(), alpha=4, param_dtype=float)
sa = nk.sampler.MetropolisExchange(hi, graph=g, n_chains=16)
vs = nk.vqs.MCState(sa, ma, n_samples=1008, n_discard_per_chain=10)

print(vs.n_parameters)
```

### Pitfalls and fixes
- Constrained Hilbert space with incompatible sampler can violate effective exploration; use exchange/conserving rules when needed. (`docs/user-guides/hilbert.md`)
- Non-Flax models can work but are documented as experimental; start with Flax for baseline correctness. (`docs/user-guides/varstate.md`)
- OOM during expectation/grad: reduce `chunk_size` on `MCState`. (`docs/user-guides/varstate.md`)
- Mixing operator and Hilbert spaces leads to immediate type/shape failures in driver construction. (`docs/user-guides/drivers.md`, `netket/driver/vmc.py`)
- Manual parameter mutation without copying nested trees can cause unintended side effects; use `flax.core.copy`. (`docs/user-guides/varstate.md`)

### Convergence and validation checks
- `vstate.n_parameters` and parameter tree structure are stable after init/update.
- Sampler output shape matches `(chain_length, n_chains_per_rank, hilbert.size)` semantics.
- Acceptance is non-pathological and not stuck near zero for long warmup.
- Small-system cross-check with `FullSumState` or exact sampler when feasible.

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Prioritize consistency checks across graph/hilbert/operator/model/sampler choices.

## Primary documentation references
- `docs/user-guides/hilbert.md`
- `docs/user-guides/operator.md`
- `docs/user-guides/varstate.md`
- `docs/user-guides/sampler.ipynb`
- `docs/advanced/custom_models.md`
- `docs/advanced/custom_hilbert_constraints.md`
- `docs/api/models.md`
- `docs/api/geometry.md`
- `docs/api/errors.md`

## Workflow
- Start from user guides for composition rules and supported combinations.
- Use API docs for exact constructor signatures and class inventory.
- If unresolved, inspect `references/doc_map.md`, then source entry points.
- Cite exact docs paths and clearly separate inferred implementation behavior.

## Tutorials and examples
- `Examples/Ising1d/ising1d.py`
- `Examples/Heisenberg1d/heisenberg1d.py`
- `docs/tutorials`

## Test references
- `test/variational`
- `test/operator`
- `test/sampler`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/hilbert/__init__.py` and `netket/hilbert/constraint/__init__.py` (Hilbert families and constraints)
- `netket/models/__init__.py` and `netket/models/utils.py` (model registration/helpers)
- `netket/models/rbm.py` and `netket/models/tensor_networks/mps.py` (canonical model implementations)
- `netket/operator/__init__.py` and `netket/operator/_graph_operator.py` (operator entry and graph-based implementation)
- `netket/sampler/metropolis.py` and `netket/sampler/rules/local.py` (sampler core and transition rules)
- `netket/vqs/mc/mc_state/state.py` (state init, sample count/chunk behavior)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
