---
name: netket-build-and-install
description: This skill should be used when users ask about build and install in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Build and Install

## High-Signal Playbook
### Route conditions
- Route to `netket-getting-started` for first tutorial execution flow.
- Route to `netket-parallel-hpc` for multi-node/multi-GPU launch/runtime issues.
- Route to `netket-api-and-scripting` for post-install API usage or serialization questions.

### Triage questions
- Which Python version is active (NetKet needs 3.11+)? (`docs/install.md`)
- Are they using `pip`/`uv` (supported) or `conda` (discouraged)? (`README.md`, `docs/install.md`)
- CPU-only or GPU install target?
- Is this a stable release install or Git development install?
- Is the environment local workstation or HPC cluster?
- Do they fail at install time, import time, or first run?

### Canonical workflow
1. Confirm Python `>=3.11` and a clean non-conda environment (`docs/install.md`).
2. Install with `uv add netket` or `pip install netket` (`docs/install.md`).
3. For GPU, install GPU-enabled JAX (or `netket[cuda]`) and avoid manual CUDA toolkit coupling (`docs/install.md`).
4. Verify import/version (`python -c "import netket; print(netket.__version__)"`).
5. Verify device visibility (`python -c 'import jax; print(jax.devices())'`).
6. Run diagnostic dump on failures (`python -m netket.tools.info`).
7. On clusters, prefer `uv`, avoid loading system CUDA modules unless site policy requires it (`docs/install.md`, `docs/parallel-multinode.md`).

### Minimal working example
```bash
pip install --upgrade pip
pip install netket
python -c "import netket; print(netket.__version__)"
python -c 'import jax; print(jax.devices())'
python -m netket.tools.info
```

### Pitfalls and fixes
- Conda installs often yield stale/fragile JAX stacks; switch to `pip` or `uv`. (`docs/install.md`)
- GPU not detected after install: verify JAX installation path, not just NetKet extras. (`docs/install.md`)
- Custom CUDA module conflicts with JAX-managed CUDA wheels; remove cluster CUDA module from environment. (`docs/install.md`, `docs/parallel-multinode.md`)
- Installing development head for production runs introduces instability; pin a release for reproducibility. (`docs/install.md`)
- MPI expectations mismatch: modern NetKet distributed path is JAX distributed/sharding, not legacy MPI APIs. (`docs/parallel.md`, `netket/utils/mpi/__init__.py`)

### Convergence and validation checks
- `import netket` succeeds and version is current enough for required features.
- `jax.devices()` lists expected CPU/GPU devices.
- `python -m netket.tools.info` reports coherent versions for `jax`, `jaxlib`, `flax`, `optax`.
- A tiny example script runs to completion and writes output logs.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep guidance focused on reproducible environment setup before runtime tuning.

## Primary documentation references
- `README.md`
- `docs/install.md`
- `docs/parallel.md`
- `docs/parallel-mpi.md`
- `docs/parallel-multinode.md`
- `docs/philosophy.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic list.
- For runtime/distributed issues, cross-check with `docs/sharp-bits.md` and `netket-parallel-hpc`.
- If ambiguity remains, inspect `references/source_map.md` and source entry points below.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `Examples`
- `docs/tutorials`
- `docs/vmc-from-scratch`

## Test references
- `test`
- `test_sharding`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/tools/info.py` (environment diagnostics command)
- `netket/utils/_dependencies_check.py` (dependency checks)
- `netket/utils/mpi/__init__.py` (legacy MPI deprecation surface)
- `netket/utils/mpi/mpi.py` (current MPI compatibility stubs)
- `netket/utils/mpi/primitives.py` (no-op reduction primitives under removed MPI path)
- `netket/jax/sharding/__init__.py` (current distributed/sharding utility exports)
- `netket/operator/_local_operator/compile_helpers.py` (compile-time helpers tied to operator internals)
- Prefer targeted search: `rg -n "<symbol_or_keyword>" netket`
