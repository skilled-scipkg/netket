# netket source map: Assets

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `docs/conf.py` - `autodoc_skip_member`, `setup` for Sphinx registration behavior.
- `docs/sphinx_extensions/link_to_source.py` - `linkcode_resolve`, `get_object_from_path`.
- `docs/sphinx_extensions/netket_citations.py` - `CitationsListDirective`, `setup`.
- `docs/sphinx_extensions/nk_list_config_options.py` - `ConfigOptionDirective`, `create_field_item`.
- `docs/sphinx_extensions/flax_module/fmodule.py` - `render_module`, `FlaxModuleDirective`.
- `docs/sphinx_extensions/custom_inheritance_diagram/inheritance_diagram.py` - `InheritanceGraph`, `setup`.

## Fast probes
- `rg -n "def setup|class .*Directive" docs/conf.py docs/sphinx_extensions`
- `rg -n "def linkcode_resolve|def render_module" docs/sphinx_extensions`

## Validation checkpoints
- Docs asset bugs can be tied to one extension/config function.
- Template rendering issues map back to directive or config setup code.
