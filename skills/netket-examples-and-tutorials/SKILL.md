---
name: netket-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Route to `netket-getting-started` for install/import failures before running examples.
- Route to `netket-simulation-workflows` when the question shifts to convergence tuning.
- Route to `netket-parallel-hpc` for multi-process launches and sharding examples.

### Triage questions
- Notebook tutorial or standalone Python example?
- Ground-state VMC, dynamics, infidelity, or fermionic workflows?
- Single-device run or distributed/sharded run?

### Canonical workflow
1. Start from `docs/tutorials/index.md` or the closest example directory.
2. Run the smallest example in the selected family first.
3. Capture run output/log files and compare with expected trends.
4. Only then move to larger systems or advanced examples.
5. Escalate to `references/source_map.md` if tutorial behavior diverges from docs.

### Minimal operational checks
```bash
python Examples/Ising1d/ising1d.py
python Examples/Heisenberg1d/heisenberg1d.py
```

### Validation checkpoints
- Scripts execute end-to-end and produce log/output files.
- Energy/observable traces evolve and are finite.
- Example settings are reproducible when rerun with same seeds/config.

## Scope
- Handle tutorial/example selection and practical execution steps.
- Keep guidance runnable with concrete command paths.

## Primary documentation references
- `docs/tutorials/index.md`
- `docs/tutorials/symmetries/index.md`
- `docs/tutorials/gs-ising.ipynb`
- `docs/tutorials/gs-heisenberg.ipynb`
- `Examples/Autoregressive/README.md`

## Workflow
- Start from the exact tutorial or example requested by the user.
- Use `references/doc_map.md` for adjacent examples in the same family.
- Escalate to `references/source_map.md` for implementation-level divergence checks.

## Tutorials and examples
- `Examples`
- `docs/tutorials`
- `docs/vmc-from-scratch`

## Test references
- `test/driver`
- `test/variational`
- `test/sampler`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/driver/vmc.py` (`VMC.compute_loss_and_update`)
- `netket/_src/driver/vmc_sr.py` (`VMC_SR.compute_loss_and_update`)
- `netket/sampler/metropolis.py` (`MetropolisLocal`, `MetropolisExchange`)
- `netket/models/rbm.py` (`RBM`, `RBMSymm`)
- `netket/models/autoreg.py` (`ARNNSequential`, `ARNNDense`)
- `netket/experimental/observable/infidelity/expect.py` (`infidelity`)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket Examples`
