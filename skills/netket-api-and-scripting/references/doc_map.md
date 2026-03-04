# netket documentation map: API and Scripting

## Public API and usage docs
- `docs/api/api.md` - canonical public API module map.
- `docs/api/api-stability.md` - stability contract and semver expectations.
- `docs/api/vqs.md` - variational state APIs.
- `docs/api/drivers.md` - driver APIs (`VMC`, `VMC_SR`, others).
- `docs/api/optimizer.md` - optimizers and preconditioners.
- `docs/api/logging.md` - loggers and persistence hooks.
- `docs/api/callbacks.md` - callback interfaces and built-ins.
- `docs/api/sampler.md` - sampler classes and rules.
- `docs/user-guides/varstate.md` - practical state construction and serialization context.
- `docs/user-guides/drivers.md` - run-loop usage patterns.
- `docs/user-guides/configurations.md` - environment/config flags affecting API behavior.

## Startup snippet
```python
import netket as nk
print(nk.__version__)
print(nk.driver.VMC)
print(nk.vqs.MCState)
```

## Validation checkpoints
- API calls are from documented modules in `docs/api/api.md`.
- Stability-sensitive usage aligns with `docs/api/api-stability.md`.
- Serialization/logging path is explicitly chosen before long runs.
