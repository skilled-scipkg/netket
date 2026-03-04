# netket source map: Build and Install

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/tools/info.py` - `info`, `_jax_backends`, `_fmt_device` diagnostics.
- `netket/utils/_dependencies_check.py` - `create_msg` dependency mismatch diagnostics.
- `netket/utils/version_check.py` - `module_version`, `version_string`, `version_tuple`.
- `netket/vqs/mc/mc_state/state.py` - `check_chunk_size` for sample/chunk validation errors.
- `netket/jax/sharding/fixed_sharding_utils.py` - `with_samples_sharding_constraint`, `gather`.
- `netket/utils/mpi/primitives.py` - `mpi_sum_jax`, `mpi_allreduce_sum_jax`, `mpi_bcast_jax`.
- `netket/utils/mpi/__init__.py` - deprecation bridge exposing MPI removal behavior.

## Fast probes
- `rg -n "def info|def _jax_backends" netket/tools/info.py`
- `rg -n "def module_version|def version_string" netket/utils/version_check.py`
- `rg -n "def mpi_.*jax" netket/utils/mpi/primitives.py`

## Validation checkpoints
- Installation/runtime diagnostics can be reproduced with callable utilities above.
- Distributed/install guidance aligns with current deprecation and sharding utilities.
