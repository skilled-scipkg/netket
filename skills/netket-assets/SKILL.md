---
name: netket-assets
description: This skill should be used when users ask about assets in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Assets

## High-Signal Playbook
### Route conditions
- Route to `netket-developer-guide` for broader Sphinx/dev tooling changes.
- Route to `netket-api-and-scripting` when docs rendering issues originate from API object definitions.
- Route to `netket-getting-started` if the request is about running simulations (not docs assets).

### Triage questions
- Is the issue in autosummary templates, Sphinx extensions, or static assets?
- Is the user changing how API docs are rendered for Flax/module wrappers?
- Is the failure in docs build (`make html`) or runtime rendering in generated pages?

### Canonical workflow
1. Start from template docs in `docs/assets/templates/autosummary`.
2. Verify Sphinx configuration and extension wiring in `docs/conf.py`.
3. Inspect extension functions in `docs/sphinx_extensions` for rendering/link/citation behavior.
4. Run a local docs build and confirm generated HTML includes the expected sections.
5. If unresolved, inspect `references/source_map.md` functions directly.

### Minimal operational checks
```bash
cd docs
make html
```

### Validation checkpoints
- Docs build finishes without extension import errors.
- Generated API pages include expected autosummary sections.
- Link-to-source and citation directives render correctly.

## Scope
- Handle documentation assets/templates and Sphinx extension behavior.
- Keep this skill docs-tooling focused, not simulation-execution focused.

## Primary documentation references
- `docs/assets/templates/autosummary/flax_module_or_default.rst`
- `docs/assets/templates/autosummary/flax_module.rst`
- `docs/assets/templates/autosummary/flax_function_wrap.rst`
- `docs/assets/templates/autosummary/class.rst`
- `docs/conf.py`

## Workflow
- Start with the primary references above.
- Use `references/doc_map.md` for adjacent assets and template files.
- Use `references/source_map.md` when debugging extension functions.

## Tutorials and examples
- `docs/README.md`

## Test references
- `test`

## Optional deeper inspection
- `docs/sphinx_extensions`

## Source entry points for unresolved issues
- `docs/conf.py` (`autodoc_skip_member`, `setup`)
- `docs/sphinx_extensions/link_to_source.py` (`linkcode_resolve`, `get_object_from_path`)
- `docs/sphinx_extensions/netket_citations.py` (`CitationsListDirective`, `setup`)
- `docs/sphinx_extensions/nk_list_config_options.py` (`ConfigOptionDirective`)
- `docs/sphinx_extensions/flax_module/fmodule.py` (`render_module`, `FlaxModuleDirective`)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" docs/sphinx_extensions docs/conf.py`
