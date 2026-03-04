---
name: netket-simulation-workflows
description: This skill should be used when users ask about simulation workflows in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Route to `netket-inputs-and-modeling` if Hamiltonian/model/sampler definitions are still undecided.
- Route to `netket-parallel-hpc` for multi-node/multi-GPU launch and distributed deadlocks.
- Route to `netket-api-and-scripting` for low-level logger/callback implementation details.

### Triage questions
- Ground-state (`VMC`/`VMC_SR`) or steady-state/infidelity workflow?
- Is SR needed, and if yes are `diag_shift` and solver choices already set?
- Which sampler and chain settings are being used (`n_chains`, `n_samples`, discard)?
- What output format is required: runtime-only, JSON, state checkpoints, tensorboard?
- Is the issue convergence quality, runtime stability, or distributed execution behavior?
- Is reproducibility required (fixed seeds/version pinning)?

### Canonical workflow
1. Construct operator, optimizer, variational state explicitly (`docs/user-guides/drivers.md`, `docs/user-guides/varstate.md`).
2. Pick driver: `VMC` for baseline, `VMC_SR` for modern SR/minSR flow (`docs/api/drivers.md`, `docs/user-guides/sr.md`).
3. Configure sampling knobs: `n_samples`, `n_discard_per_chain`, `n_chains` (`docs/user-guides/varstate.md`, `docs/user-guides/sampler.ipynb`).
4. Configure preconditioning: SR/diag shift/schedule and solver (`docs/user-guides/sr.md`, `docs/api/optimizer.md`).
5. Run with explicit logger/callback strategy (`docs/user-guides/drivers.md`, `docs/api/logging.md`, `docs/api/callbacks.md`).
6. Validate trends (energy/error/acceptance) and checkpoint artifacts.
7. For failures, use callback hooks and sharp-bits guidance before source deep dive.

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

op = nk.optimizer.Sgd(learning_rate=0.01)
driver = nk.driver.VMC_SR(ha, op, variational_state=vs, diag_shift=0.1)
log = nk.logging.JsonLog("run/heisenberg")

driver.run(n_iter=300, out=log)
```

### Pitfalls and fixes
- Legacy callback signature confusion: modern hook-based callback API has explicit hook stages; old callable callbacks are wrapped. (`docs/advanced/custom_callbacks.md`)
- SR with too few samples vs parameters can produce unstable updates; increase samples or use minSR/VMC_SR defaults. (`netket/driver/vmc.py`, `docs/user-guides/sr.md`)
- `n_samples`/chains mismatch silently rounds upward; account for effective sample count in cost estimates. (`netket/vqs/mc/mc_state/state.py`)
- JAX distributed deadlocks often come from mismatched process setup or rank-gated JAX array ops. (`docs/parallel-multinode.md`, `Examples/Sharding/multi_process.py`)
- Sharp-bits issues (NaNs/precision/platform) should be checked before changing algorithms. (`docs/sharp-bits.md`)

### Convergence and validation checks
- Track `Energy` mean + error bars and ensure trend is monotonic enough for chosen step size.
- Track sampler acceptance and watch for collapse/stagnation.
- Verify output artifacts: `.log` JSON exists and parses; `.mpack`/state checkpoints exist when configured.
- Re-run short continuation from checkpoint/log to verify reproducible progression.
- In distributed runs, verify rank/device diagnostics match expected topology before optimization.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Prioritize robust run-loop patterns and observability/checkpointing.

## Primary documentation references
- `docs/user-guides/drivers.md`
- `docs/user-guides/varstate.md`
- `docs/user-guides/sampler.ipynb`
- `docs/user-guides/sr.md`
- `docs/advanced/custom_callbacks.md`
- `docs/api/drivers.md`
- `docs/api/logging.md`
- `docs/api/callbacks.md`
- `docs/sharp-bits.md`

## Workflow
- Start with docs above and pick a single recommended run path.
- For alternative algorithms (NTK/minSR, infidelity, steady-state), branch only after baseline path is valid.
- If unresolved, inspect `references/doc_map.md` and then source entry points.
- Cite exact docs paths; call out when behavior comes from source internals.

## Tutorials and examples
- `Examples/Heisenberg1d/heisenberg1d.py`
- `Examples/Ising1d/ising1d.py`
- `docs/tutorials/gs-ising.ipynb`

## Test references
- `test/driver/test_vmc.py`
- `test/driver/test_vmc_ngd.py`
- `test/driver/test_srt.py`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/driver/vmc.py` (baseline driver update logic)
- `netket/_src/driver/vmc_sr.py` (modern SR/minSR workflow)
- `netket/_src/driver/abstract_variational_driver.py` (run loop, step/reset/log plumbing)
- `netket/vqs/mc/mc_state/state.py` (sampling cache, sample/discard/chunk semantics)
- `netket/optimizer/sr.py` (preconditioner interface and schedule handling)
- `netket/optimizer/qgt/default.py` (QGT auto-selection heuristics)
- `netket/logging/json_log.py`, `netket/logging/state_log.py`, `netket/_src/callbacks/save_state.py` (checkpoint/output behavior)
- `netket/_src/callbacks/base.py` and `netket/callbacks/__init__.py` (callback hook surface)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
