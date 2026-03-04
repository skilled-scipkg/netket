# netket source map: Parallel and HPC

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/jax/sharding/fixed_sharding_utils.py` - `distribute_to_devices_along_axis`, `shard_along_axis`, `gather`.
- `netket/jax/sharding/debug.py` - `inspect` for inside-jit sharding diagnostics.
- `netket/utils/struct/pytree_serialization_sharding.py` - `from_flax_state_dict_sharding_strict`, `from_flax_state_dict_sharding_relaxed`.
- `netket/_src/callbacks/auto_slurm_requeue.py` - `get_time_left`, `is_requeueable`, `AutoSlurmRequeue`.
- `netket/_src/callbacks/save_state.py` - `SaveVariationalState.on_run_end` for checkpoint write paths.
- `netket/logging/json_log.py` - `JsonLog.__call__`, `JsonLog.flush`.
- `netket/utils/mpi/primitives.py` - `mpi_sum_jax`, `mpi_allreduce_sum_jax`, `mpi_scatter_jax`.
- `netket/utils/mpi/__init__.py` - MPI deprecation surface for legacy code triage.

## Fast probes
- `rg -n "def distribute_to_devices_along_axis|def gather" netket/jax/sharding/fixed_sharding_utils.py`
- `rg -n "class AutoSlurmRequeue|def get_time_left" netket/_src/callbacks/auto_slurm_requeue.py`
- `rg -n "def mpi_.*jax" netket/utils/mpi/primitives.py`

## Validation checkpoints
- Distributed failures are explained using explicit sharding/checkpoint/mpi functions.
- Rank/device behavior is verified with code paths listed above before scaling jobs.
