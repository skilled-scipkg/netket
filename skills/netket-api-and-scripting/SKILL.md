---
name: netket-api-and-scripting
description: This skill should be used when users ask about api and scripting in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: API and Scripting

## High-Signal Playbook
### Route conditions
- Route to `netket-inputs-and-modeling` for model/Hilbert/constraint design decisions.
- Route to `netket-simulation-workflows` for end-to-end run orchestration and callback policies.
- Route to `netket-parallel-hpc` when API usage is blocked by distributed runtime/sharding behavior.

### Triage questions
- Are they asking public stable APIs or internals/experimental modules? (`docs/api/api-stability.md`)
- Do they need class-level API map (`netket.vqs`, `netket.driver`, `netket.optimizer`, `netket.logging`)?
- Which variational state type: `MCState`, `MCMixedState`, or `FullSumState`?
- Which driver path: `VMC`, `VMC_SR`, `SteadyState`, or infidelity fitting?
- Do they need serialization/checkpointing or just runtime logging?
- Are they using pure-Flax models or custom framework wrappers?

### Canonical workflow
1. Confirm API stability expectations and public surface (`docs/api/api-stability.md`, `docs/api/api.md`).
2. Map the request to module entry points: `nk.vqs`, `nk.driver`, `nk.optimizer`, `nk.logging`, `nk.sampler`.
3. Build the state explicitly (`MCState`/`FullSumState`) before constructing drivers (`docs/user-guides/varstate.md`, `docs/user-guides/drivers.md`).
4. Choose optimizer/preconditioner (`Sgd` + optional `SR` or use `VMC_SR`) (`docs/api/optimizer.md`, `docs/api/drivers.md`).
5. Attach logging/output channel (`RuntimeLog`, `JsonLog`, `StateLog`, `TensorBoardLog`) (`docs/api/logging.md`).
6. For persistence, serialize with Flax or use logger state saving paths (`docs/user-guides/varstate.md`).
7. Escalate to source only for behavior not explicit in docs (state reset semantics, logging flush behavior, callback ordering).

### Minimal working example
```python
import flax
import netket as nk

hi = nk.hilbert.Spin(0.5, N=10)
sa = nk.sampler.MetropolisLocal(hi, n_chains=16)
ma = nk.models.RBM(alpha=1)
vs = nk.vqs.MCState(sa, ma, n_samples=512, n_discard_per_chain=10)

gs = nk.driver.VMC(
    nk.operator.Ising(hi, nk.graph.Chain(10), h=1.0),
    nk.optimizer.Sgd(learning_rate=0.02),
    variational_state=vs,
)
log = nk.logging.JsonLog("run/api_demo")
gs.run(n_iter=20, out=log)

with open("run/vstate.mpack", "wb") as f:
    f.write(flax.serialization.to_bytes(vs))
```

### Pitfalls and fixes
- Using underscored/private or `experimental` modules as stable API will break across minor updates. (`docs/api/api-stability.md`)
- Non-Flax model wrappers are supported but still more fragile than standard Flax modules. (`docs/user-guides/varstate.md`)
- Runtime mutation of unsupported config keys can error; set env vars before import when needed. (`docs/user-guides/configurations.md`)
- `n_samples` is rounded to match chain/device layout; treat warnings as expected shape alignment behavior. (`netket/vqs/mc/mc_state/state.py`)
- `netket.nn` mirrors/patches upstream functionality; version pinning of `jax/flax/optax` is important for reproducibility. (`docs/api/api-stability.md`)

### Convergence and validation checks
- `driver.energy` (or target metric) trend and error bars decrease across iterations.
- Logger output contains expected keys (`Energy`, observables, acceptance where applicable).
- Reloaded serialized variational state reproduces shapes and can run one extra step.
- API usage stays within documented modules listed in `docs/api/api.md`.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Prioritize public API maps and common scripting patterns before implementation details.

## Primary documentation references
- `docs/api/api.md`
- `docs/api/api-stability.md`
- `docs/api/vqs.md`
- `docs/api/drivers.md`
- `docs/api/optimizer.md`
- `docs/api/logging.md`
- `docs/api/sampler.md`
- `docs/user-guides/varstate.md`
- `docs/user-guides/drivers.md`
- `docs/user-guides/configurations.md`

## Workflow
- Start with API docs for public signatures and module boundaries.
- Use user guides for recommended construction order and runtime patterns.
- If unresolved, inspect `references/doc_map.md`, then `references/source_map.md`.
- Cite exact documentation paths and call out when behavior is implementation-derived.

## Tutorials and examples
- `Examples`
- `docs/tutorials`
- `docs/vmc-from-scratch`

## Test references
- `test/driver`
- `test/variational`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/vqs/__init__.py` (public vqs exports)
- `netket/vqs/base.py` (variational-state contract, reset/parameters semantics)
- `netket/vqs/mc/mc_state/state.py` (MCState constructor, samples/chunking behavior)
- `netket/vqs/full_summ/state.py` (deterministic full-summation state)
- `netket/driver/vmc.py` (baseline VMC flow)
- `netket/_src/driver/abstract_variational_driver.py` (run loop, callback/logging integration)
- `netket/_src/driver/vmc_sr.py` (SR/minSR driver internals)
- `netket/logging/json_log.py` and `netket/logging/runtime_log.py` (logging and flush behavior)
- `netket/_src/callbacks/save_state.py` (portable variational-state checkpoint callback)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
