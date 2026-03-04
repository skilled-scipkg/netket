# netket documentation map: Developer Guide

## Core developer docs
- `docs/developer-guides/index.md` - guide index for contributors.
- `docs/developer-guides/contributing.md` - PR and contribution workflow.
- `docs/developer-guides/writing-tests.md` - test structure and conventions.
- `docs/developer-guides/documentation.md` - docs update workflow.
- `docs/advanced/custom_expect.md` - expectation-dispatch customization.
- `docs/advanced/custom_models.md` - custom model extension pattern.
- `docs/advanced/custom_callbacks.md` - callback hook lifecycle.

## Focused validation commands
```bash
pytest -q test/driver/test_vmc.py
pytest -q test/variational -k expect
```

## Validation checkpoints
- Extension behavior is covered by targeted tests.
- Hook/dispatch behavior is reproducible and documented.
- Changes remain consistent with API-stability boundaries.
