---
name: netket-index
description: This skill should be used when users ask how to use netket and the correct generated documentation skill must be selected before going deeper into source code.
---

# netket Skills Index

## Route the request
- First classify user intent, then hand off to one primary topic skill.
- Keep answers docs-first; use source escalation only when docs are insufficient.

## Intent-to-skill routing
- `netket-getting-started`: first install, first runnable script, first troubleshooting checks.
- `netket-build-and-install`: environment setup, package install/upgrade, dependency and tooling validation.
- `netket-simulation-workflows`: end-to-end VMC/driver runs, callbacks, logging, checkpointing, result interpretation.
- `netket-inputs-and-modeling`: Hilbert/operator/model construction, constraints, variational state setup.
- `netket-api-and-scripting`: API surface discovery, import/module entry points, scripting and serialization patterns.
- `netket-user-guides`: in-depth conceptual usage (SR/QGT, operators, utility modules, module-level guides).
- `netket-parallel-hpc`: multi-GPU, multi-node, distributed runtime setup/debug.
- `netket-examples-and-tutorials`: worked examples/tutorial walkthroughs.
- `netket-theory-and-methods`: theory-first or algorithmic-method questions.
- `netket-developer-guide`: contribution, internal architecture, testing/developer workflows.
- `netket-assets`: docs template/assets questions.
- `netket-advanced-topics`: sparse/edge topics (advanced index, changelog, sharding test docs, vmc-from-scratch index, general docs landing).

## Docs-first escalation protocol
1. Start from the selected topic skill `Primary documentation references`.
2. If needed, expand within that skill's `references/doc_map.md`.
3. Only if ambiguity remains, inspect that skill's `references/source_map.md` entry points.
4. Use targeted symbol search in source (`rg -n "<symbol_or_keyword>" netket`).

## Fast simulation startup handoff
```bash
pip install netket
python -c "import netket; print(netket.__version__)"
python Examples/Ising1d/ising1d.py
```

## Explicit repository roots
- Documentation root: `docs`
- Tutorials roots: `docs/tutorials`, `docs/vmc-from-scratch`
- Examples root: `Examples`
- Behavior/regression roots: `test`, `test_sharding`
- Source root for escalation: `netket`

## Notes for routing quality
- Prefer one best skill over spreading across many skills.
- If a request spans topics, answer from the primary skill and add one explicit cross-route.
- Treat `docs/distributed-computing.md` as redirecting to `docs/parallel.md`.
- Use `references/doc_map.md` and `references/source_map.md` in this skill for top-level cross-topic inventory.
