# netket documentation map: Getting Started

## Read in this order for first simulation
- `README.md` - installation and project overview.
- `docs/install.md` - supported install paths and GPU notes.
- `docs/tutorials/index.md` - tutorial index and progression.
- `docs/tutorials/gs-ising.ipynb` - first tutorial workflow.
- `Examples/Ising1d/ising1d.py` - first script run path.
- `docs/parallel.md` - when moving beyond single-device execution.

## Minimal commands
```bash
pip install netket
python -c "import netket; print(netket.__version__)"
python Examples/Ising1d/ising1d.py
```

## Validation checkpoints
- Import/version check succeeds.
- Example run completes and writes output logs.
- Initial metrics are finite and evolve (not all NaN/inf/constant).
