---
name: netket-advanced-topics
description: This skill should be used for sparse advanced topics in netket that were each previously one-doc skills (advanced index, changelog, vmc-from-scratch index, sharding tests, and docs landing pages), with docs-first routing and selective source escalation.
---

# netket: Advanced Topics

## High-Signal Playbook
### Route conditions
- Route to `netket-getting-started` for first install and first example execution.
- Route to `netket-simulation-workflows` for VMC tuning, callbacks, and convergence troubleshooting.
- Route to `netket-parallel-hpc` for multi-process and sharding runtime failures.

### Triage questions
- Is the request about release changes (`docs/changelog.md`) or advanced extension APIs (`docs/advanced/index.md`)?
- Is the user following VMC-from-scratch notebooks or troubleshooting production jobs?
- Are failures tied to sharding tests and distributed launch scripts?

### Canonical workflow
1. Start from one exact doc path in `Primary documentation references`.
2. For version regressions, compare behavior against `docs/changelog.md` and confirm `netket.__version__`.
3. For notebook-guided derivations, follow `docs/vmc-from-scratch/index.md` and run the matching notebook/example.
4. For sharding issues, use `test_sharding/readme.md` and run the smallest sharding script first.
5. Escalate to `references/source_map.md` only for behavior not explicit in docs.

### Minimal operational checks
```bash
python -c "import netket; print(netket.__version__)"
bash test_sharding/run_test_sharding_1cpu.sh
```

### Validation checkpoints
- Installed version matches the expected changelog section.
- Sharding smoke test completes before scaling to larger jobs.
- Any source-level conclusion points to a concrete function/class in `references/source_map.md`.

## Scope
- Handle low-frequency advanced docs and edge routing.
- Keep answers concise and route quickly to higher-signal topic skills when needed.

## Primary documentation references
- `docs/advanced/index.md`
- `docs/changelog.md`
- `docs/index.md`
- `docs/vmc-from-scratch/index.md`
- `test_sharding/readme.md`

## Workflow
- Start docs-first from the exact reference above.
- Use `references/doc_map.md` for nearby docs in this topic.
- Escalate to `references/source_map.md` for implementation behavior checks only.

## Tutorials and examples
- `docs/vmc-from-scratch`
- `docs/tutorials`
- `Examples`

## Test references
- `test_sharding`
- `test`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/_src/driver/abstract_variational_driver.py` (`AbstractVariationalDriver.run`, callback orchestration)
- `netket/driver/vmc.py` (`VMC.compute_loss_and_update`, baseline VMC step behavior)
- `netket/_src/driver/vmc_sr.py` (`VMC_SR.compute_loss_and_update`, SR/minSR path)
- `netket/_src/callbacks/save_state.py` (`SaveVariationalState.before_parameter_update`)
- `netket/jax/sharding/fixed_sharding_utils.py` (`distribute_to_devices_along_axis`, `gather`)
- `netket/utils/struct/pytree_serialization_sharding.py` (`from_flax_state_dict_sharding_strict`)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
