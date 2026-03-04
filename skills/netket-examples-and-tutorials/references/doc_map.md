# netket documentation map: Examples and Tutorials

## Tutorial and example entry docs
- `docs/tutorials/index.md` - tutorial index and topic overview.
- `docs/tutorials/gs-ising.ipynb` - ground-state Ising tutorial notebook.
- `docs/tutorials/gs-heisenberg.ipynb` - Heisenberg tutorial notebook.
- `docs/tutorials/symmetries/index.md` - symmetry tutorial landing.
- `docs/vmc-from-scratch/index.md` - notebook path for manual VMC internals.
- `Examples/Autoregressive/README.md` - autoregressive example overview.
- `Examples/Ising1d/ising1d.py` - canonical minimal script example.
- `Examples/Heisenberg1d/heisenberg1d.py` - standard VMC workflow example.
- `Examples/Sharding/multi_process.py` - distributed/sharding example.

## Runnable commands
```bash
python Examples/Ising1d/ising1d.py
python Examples/Heisenberg1d/heisenberg1d.py
```

## Validation checkpoints
- Example scripts complete and produce finite metric traces.
- Tutorial object choices (sampler/model/driver) map to docs explanations.
- Distributed examples are only attempted after local example success.
