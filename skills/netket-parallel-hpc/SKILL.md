---
name: netket-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Parallel and HPC

## High-Signal Playbook
### Route conditions
- Route to `netket-build-and-install` for base environment/JAX installation failures.
- Route to `netket-simulation-workflows` for driver-level convergence/logging once runtime is healthy.
- Route to `netket-getting-started` for single-device onboarding before distributed scaling.

### Triage questions
- Single-node multi-GPU, multi-node multi-GPU, or CPU-only distributed run?
- Scheduler/environment: SLURM, local `djaxrun`, or custom launcher?
- Is `jax.distributed.initialize()` called before importing/allocating NetKet arrays?
- Do process and device counts match expected topology?
- Are failures deadlocks, wrong device visibility, or incorrect output/I/O behavior?
- Are they using legacy MPI APIs (`netket.utils.mpi`) instead of current JAX distributed path?

### Canonical workflow
1. Choose execution mode from `docs/parallel.md` (single-node GPU, multi-node GPU, MPI backend CPU).
2. Initialize distributed JAX at process start and print diagnostics (`process_index/count`, `devices`, `local_devices`) (`docs/parallel-multinode.md`).
3. For SLURM multi-node GPU, enforce `--ntasks-per-node == GPUs per node` and use `srun` (`docs/parallel-multinode.md`).
4. For CPU MPI backend, install/import `mpibackend4jax` before JAX import (`docs/parallel-mpi.md`).
5. Keep custom I/O rank-safe (root-rank write or NetKet loggers).
6. Validate with local multi-process smoke test (`djaxrun --simple -np N ...`) before cluster jobs.

### Minimal working example
```python
import jax
jax.distributed.initialize()

print(f"[{jax.process_index()}/{jax.process_count()}] devices: {jax.devices()}", flush=True)
print(f"[{jax.process_index()}/{jax.process_count()}] local: {jax.local_devices()}", flush=True)

import netket as nk
# continue with normal NetKet construction...
```

### Pitfalls and fixes
- Deadlock at startup often means inter-node communication is blocked or launcher config is inconsistent. (`docs/parallel-multinode.md`, `docs/sharp-bits.md`)
- Using `--gpus-per-task` with auto JAX init can misconfigure device mapping; use `--ntasks-per-node` with `--gres=gpu:N`. (`docs/parallel-multinode.md`)
- Printing/operating on sharded arrays from only rank 0 can deadlock; replicate/gather or keep JAX ops on all ranks. (`Examples/Sharding/multi_process.py`)
- Legacy `netket.utils.mpi` module is deprecated and not the primary distributed interface; use JAX distributed/sharding APIs. (`netket/utils/mpi/__init__.py`, `docs/parallel.md`)
- CPU MPI backend is experimental and CPU-only; avoid mixing it with GPU workflows. (`docs/parallel-mpi.md`)

### Convergence and validation checks
- Startup diagnostics show expected `[i/N]` for all ranks and expected total device count.
- `jax.local_devices()` and scheduler allocation match exactly.
- Test write path produces one coherent output set (no clobbered multi-rank writes).
- Small distributed run completes before launching expensive production job.

## Scope
- Handle questions about MPI/OpenMP/GPU execution, scaling, and batch systems.
- Focus on distributed setup correctness and deadlock prevention.

## Primary documentation references
- `docs/parallel.md`
- `docs/parallel-multigpu.md`
- `docs/parallel-multinode.md`
- `docs/parallel-mpi.md`
- `docs/distributed-computing.md`
- `docs/sharp-bits.md`
- `test_sharding/readme.md`

## Workflow
- Start from mode selection in `docs/parallel.md`.
- Validate initialization and topology before touching optimization logic.
- For unresolved behavior, inspect `references/doc_map.md` then source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `Examples/Sharding/multi_process.py`
- `docs/tutorials`

## Test references
- `test_sharding`
- `test/driver`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/jax/sharding/__init__.py` (sharding public internals used across NetKet)
- `netket/jax/sharding/fixed_sharding_utils.py` (shard/gather/replication helpers)
- `netket/jax/sharding/debug.py` (in-jit sharding inspection helper)
- `netket/utils/struct/pytree_serialization_sharding.py` (checkpoint restore under sharding)
- `netket/_src/callbacks/auto_slurm_requeue.py` (cluster job requeue helper)
- `netket/logging/base.py` and `netket/logging/json_log.py` (rank-safe logging behavior)
- `netket/utils/mpi/__init__.py` (deprecation bridge for old MPI path)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
