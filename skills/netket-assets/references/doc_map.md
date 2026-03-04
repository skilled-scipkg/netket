# netket documentation map: Assets

## Docs asset and template references
- `docs/assets/templates/autosummary/class.rst` - base class autosummary template.
- `docs/assets/templates/autosummary/flax_function_wrap.rst` - Flax function wrapper template.
- `docs/assets/templates/autosummary/flax_module.rst` - Flax module rendering template.
- `docs/assets/templates/autosummary/flax_module_or_default.rst` - fallback Flax/default rendering template.
- `docs/assets/templates/layout.html` - docs layout template.
- `docs/conf.py` - Sphinx config and extension registration.
- `docs/README.md` - docs build usage and notebook/doc tooling notes.

## Build command
```bash
cd docs
make html
```

## Validation checkpoints
- Template updates render in generated HTML pages.
- Extension setup in `docs/conf.py` resolves without import failures.
- Link/citation/config directives appear correctly in built docs.
