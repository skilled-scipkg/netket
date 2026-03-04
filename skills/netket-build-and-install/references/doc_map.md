# netket documentation map: Build and Install

## Installation and environment docs
- `README.md` - package intro and install entry point.
- `docs/install.md` - supported installation flows and GPU notes.
- `docs/parallel.md` - high-level distributed execution overview.
- `docs/parallel-multigpu.md` - multi-GPU basics.
- `docs/parallel-multinode.md` - multi-node launcher setup.
- `docs/parallel-mpi.md` - MPI backend caveats and usage.
- `docs/sharp-bits.md` - runtime/platform pitfalls.
- `docs/philosophy.md` - architecture context for environment choices.

## Baseline commands
```bash
python -c "import netket; print(netket.__version__)"
python -c 'import jax; print(jax.devices())'
python -m netket.tools.info
```

## Validation checkpoints
- Python version and dependency stack are compatible.
- Device visibility matches target hardware.
- Diagnostics output is coherent before simulation runs.
