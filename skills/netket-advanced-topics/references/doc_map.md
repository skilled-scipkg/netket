# netket documentation map: Advanced Topics

## Primary docs for sparse advanced requests
- `docs/advanced/index.md` - advanced extension landing and links.
- `docs/changelog.md` - versioned behavior and migration clues.
- `docs/index.md` - docs landing, support, and citation context.
- `docs/vmc-from-scratch/index.md` - notebook sequence for manual VMC construction.
- `test_sharding/readme.md` - sharding-focused test execution guidance.

## Operational shortcuts
```bash
python -c "import netket; print(netket.__version__)"
rg -n "## " docs/changelog.md | head
bash test_sharding/run_test_sharding_1cpu.sh
```

## Validation checkpoints
- Requested advanced behavior is anchored to one doc above.
- Version-dependent answers cite the exact changelog section.
- Sharding troubleshooting starts with the 1-CPU sharding test script.
