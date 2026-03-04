---
name: netket-getting-started
description: This skill should be used when users ask about getting started in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Getting Started

## High-Signal Playbook
### Route conditions
- Route to `netket-build-and-install` for environment or dependency failures.
- Route to `netket-simulation-workflows` once the user moves from first run to tuning/convergence.
- Route to `netket-parallel-hpc` for multi-GPU/multi-node setup.

### Triage questions
- Do they already have Python 3.11+ and a clean environment?
- Are they installing CPU-only or GPU-enabled stack?
- Do they want the shortest runnable example or a guided tutorial path?
- Are they blocked at install, import, or execution stage?
- Do they need quick sanity checks for correctness after first run?

### Canonical workflow
1. Install NetKet with `pip` or `uv`; avoid conda path (`README.md`, `docs/install.md`).
2. Verify install with `import netket` and version print (`docs/install.md`).
3. Verify device visibility with JAX (`docs/install.md`).
4. Run a first minimal script (`Examples/Ising1d/ising1d.py`) or first tutorial listed under `docs/tutorials/index.md`.
5. Confirm output artifacts are created and contain energy history.
6. If first run passes, route to simulation/modeling skills for next step.

### Minimal working example
```bash
pip install --upgrade pip
pip install netket
python -c "import netket; print(netket.__version__)"
python Examples/Ising1d/ising1d.py
```

### Pitfalls and fixes
- Conda installs are discouraged due to JAX packaging issues; use `pip`/`uv`. (`README.md`, `docs/install.md`)
- GPU expectation mismatch: default install may still be CPU-only JAX; check `jax.devices()`. (`docs/install.md`)
- Custom CUDA stack conflicts with JAX-managed CUDA wheels; remove conflicting CUDA module setup. (`docs/install.md`)
- Development install from Git can include unstable changes; use release install for first learning loop. (`docs/install.md`)
- First script stalls on distributed clusters due to launcher confusion; test locally first, then use parallel docs.

### Convergence and validation checks
- `python -c "import netket; print(netket.__version__)"` succeeds.
- `python -c 'import jax; print(jax.devices())'` reports expected devices.
- First example exits cleanly and writes output log files.
- Log/energy values evolve across iterations (not constant NaN/inf).

## Scope
- Handle initial setup, quickstarts, and first-run checks.
- Keep answers short and executable.

## Primary documentation references
- `README.md`
- `docs/install.md`
- `docs/tutorials/index.md`
- `docs/index.md`
- `Examples/Ising1d/ising1d.py`

## Workflow
- Start from install + first-run path.
- If the user asks for deeper explanations, route immediately to topic skills.
- Use `references/doc_map.md` for additional inventory when needed.

## Tutorials and examples
- `docs/tutorials`
- `Examples/Ising1d/ising1d.py`
- `Examples/Heisenberg1d/heisenberg1d.py`

## Test references
- `test/driver`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/__init__.py` (import surface)
- `netket/tools/info.py` (diagnostics)
- `netket/driver/vmc.py` (first-run driver behavior)
- `netket/vqs/mc/mc_state/state.py` (sampling defaults)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
