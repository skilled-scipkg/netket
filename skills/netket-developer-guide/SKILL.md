---
name: netket-developer-guide
description: This skill should be used when users ask about developer guide in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Developer Guide

## High-Signal Playbook
### Route conditions
- Route to `netket-api-and-scripting` for public API usage questions.
- Route to `netket-simulation-workflows` for production run tuning and callback policy.
- Route to `netket-parallel-hpc` for distributed execution and sharding debugging.

### Triage questions
- Is this about contribution workflow, testing strategy, or extension internals?
- Are they implementing custom expectations/models/callbacks?
- Do they need behavior guarantees (tests) before merging changes?

### Canonical workflow
1. Start with `docs/developer-guides/index.md` and pick the exact sub-guide.
2. For extension points, read `docs/advanced/custom_expect.md`, `docs/advanced/custom_models.md`, and `docs/advanced/custom_callbacks.md`.
3. Reproduce behavior with the smallest test or example script.
4. Validate with focused tests before broad test sweeps.
5. Escalate to `references/source_map.md` for function-level internals.

### Minimal operational checks
```bash
pytest -q test/driver/test_vmc.py
pytest -q test/variational -k expect
```

### Validation checkpoints
- New behavior is covered by at least one targeted test.
- Callback/expectation dispatch order is explicit and reproducible.
- Public-facing changes align with API stability notes.

## Scope
- Handle contribution workflow, internal architecture, and extension hooks.
- Prioritize reproducible implementation guidance over broad theory summaries.

## Primary documentation references
- `docs/developer-guides/index.md`
- `docs/developer-guides/contributing.md`
- `docs/developer-guides/writing-tests.md`
- `docs/developer-guides/documentation.md`
- `docs/advanced/custom_expect.md`
- `docs/advanced/custom_models.md`
- `docs/advanced/custom_callbacks.md`

## Workflow
- Start docs-first for intended extension contract.
- Use `references/doc_map.md` for nearby implementation docs.
- Use `references/source_map.md` for concrete function-level behavior checks.

## Tutorials and examples
- `Examples`
- `docs/vmc-from-scratch`

## Test references
- `test`
- `test_sharding`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/_src/driver/abstract_variational_driver.py` (`maybe_wrap_legacy_callback`, `AbstractVariationalDriver.run`)
- `netket/_src/callbacks/base.py` (`AbstractCallback` hook methods)
- `netket/jax/_expect.py` (`expect`, custom VJP path)
- `netket/vqs/base.py` (`expect`, `expect_and_grad` dispatch surface)
- `netket/vqs/mc/mc_state/expect.py` (`get_local_kernel`, `expect`)
- `netket/_src/vqs/expect_to_precision.py` (`expect_to_precision` adaptive loop)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
