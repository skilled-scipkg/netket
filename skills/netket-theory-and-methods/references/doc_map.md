# netket documentation map: Theory and Methods

## Theory-first docs
- `docs/advanced/symmetry.md` - representation theory and symmetry construction.
- `docs/user-guides/superop.md` - Lindblad formalism and superoperator workflows.
- `docs/user-guides/sr.md` - QGT/SR geometry and practical regularization.
- `docs/vmc-from-scratch/index.md` - derivation-to-implementation notebook path.
- `docs/tutorials/fidelity.ipynb` - fidelity-oriented method tutorial.

## Sanity-run commands
```bash
python Examples/FullSummation/ising.py
python Examples/DissipativeIsing1d/ising1d.py
```

## Validation checkpoints
- Symmetry constraints hold for the chosen ansatz.
- Superoperator observables are finite and interpretable.
- Small-system runs match qualitative theoretical expectations.
