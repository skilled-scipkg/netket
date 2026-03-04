# netket documentation map: User Guides

## In-depth user guide docs
- `docs/user-guides/index-modules.md` - module-level routing index.
- `docs/user-guides/hilbert.md` - Hilbert construction and constraints.
- `docs/user-guides/operator.md` - operator construction patterns.
- `docs/user-guides/varstate.md` - variational state internals and API usage.
- `docs/user-guides/drivers.md` - run-loop setup and control.
- `docs/user-guides/sr.md` - SR/QGT usage and schedules.
- `docs/user-guides/sampler.ipynb` - sampler and chain behavior.
- `docs/user-guides/utils/index.md` - utility modules and notebook links.
- `docs/user-guides/configurations.md` - runtime configuration flags.

## Practical checks
```python
import netket as nk
print(nk.optimizer.SR)
print(nk.driver.VMC_SR)
```

## Validation checkpoints
- Chosen guide matches the user’s module-level question.
- Suggested parameters (`diag_shift`, samples/chains, solver) are explicit.
- Recommendations stay inside documented stable APIs where possible.
