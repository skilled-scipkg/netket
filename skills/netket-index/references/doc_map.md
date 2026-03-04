# netket documentation map: Index Router

## Core entry docs (cross-topic)
- `docs/index.md` - top-level docs landing and navigation.
- `docs/install.md` - install and environment baseline.
- `docs/tutorials/index.md` - tutorial families and first runnable notebooks.
- `docs/user-guides/index-modules.md` - in-depth module guide index.
- `docs/api/api.md` - public API module inventory.
- `docs/parallel.md` - distributed/multi-device routing entry.
- `docs/developer-guides/index.md` - contributor and extension docs.
- `docs/advanced/index.md` - advanced customization topics.

## Skill handoff map
- `skills/netket-getting-started/SKILL.md`
- `skills/netket-build-and-install/SKILL.md`
- `skills/netket-simulation-workflows/SKILL.md`
- `skills/netket-inputs-and-modeling/SKILL.md`
- `skills/netket-api-and-scripting/SKILL.md`
- `skills/netket-user-guides/SKILL.md`
- `skills/netket-parallel-hpc/SKILL.md`
- `skills/netket-examples-and-tutorials/SKILL.md`
- `skills/netket-theory-and-methods/SKILL.md`
- `skills/netket-developer-guide/SKILL.md`
- `skills/netket-assets/SKILL.md`
- `skills/netket-advanced-topics/SKILL.md`

## Fast startup sanity commands
```bash
python -c "import netket; print(netket.__version__)"
python Examples/Ising1d/ising1d.py
```

## Validation checkpoints
- A single primary skill is selected before diving into implementation details.
- Routing doc path exists and matches user intent.
- Cross-route is explicit when request spans multiple topics.
