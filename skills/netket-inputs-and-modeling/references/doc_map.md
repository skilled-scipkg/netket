# netket documentation map: Inputs and Modeling

## Core modeling docs
- `docs/user-guides/hilbert.md` - Hilbert spaces and constraints.
- `docs/user-guides/operator.md` - operator construction rules.
- `docs/user-guides/varstate.md` - model/sampler/state composition.
- `docs/user-guides/sampler.ipynb` - sampler behavior and tuning.
- `docs/advanced/custom_models.md` - custom model implementation patterns.
- `docs/advanced/custom_hilbert_constraints.md` - custom Hilbert constraints.
- `docs/api/models.md` - model class inventory.
- `docs/api/hilbert.md` - Hilbert class inventory.
- `docs/api/operator.md` - operator class inventory.
- `docs/api/errors.md` - common modeling/shape error classes.

## Input scaffold
```python
import netket as nk

g = nk.graph.Chain(length=16, pbc=True)
hi = nk.hilbert.Spin(s=0.5, N=g.n_nodes, total_sz=0)
ha = nk.operator.Heisenberg(hi, graph=g)
```

## Validation checkpoints
- Graph/Hilbert/operator are mutually compatible.
- Sampler transition rule matches Hilbert constraints.
- `MCState` shape/sample settings are explicit before training.
