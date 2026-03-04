# netket source map: Getting Started

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/tools/info.py` - `info`, `_jax_backends` for environment diagnostics.
- `netket/utils/_dependencies_check.py` - `create_msg` for dependency mismatch details.
- `netket/vqs/mc/mc_state/state.py` - `compute_chain_length`, `check_chunk_size`, `MCState.__init__`, `MCState.sample`.
- `netket/driver/vmc.py` - `VMC.__init__`, `VMC.compute_loss_and_update`.
- `netket/_src/driver/abstract_variational_driver.py` - `AbstractVariationalDriver.run`, `reset_step`.
- `netket/logging/json_log.py` - `JsonLog.__call__`, `JsonLog.flush`.

## Fast probes
- `rg -n "def info|def _jax_backends" netket/tools/info.py`
- `rg -n "class MCState|def check_chunk_size|def sample" netket/vqs/mc/mc_state/state.py`
- `rg -n "class VMC|def compute_loss_and_update" netket/driver/vmc.py`

## Validation checkpoints
- First-run failures map to one concrete diagnostic/state/driver function.
- Fixes are verified by rerunning the minimal example after each change.
