# netket source map: API and Scripting

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/vqs/base.py` - `expect`, `expect_and_grad`, `expect_and_forces` dispatch entry points.
- `netket/vqs/mc/mc_state/state.py` - `MCState.__init__`, `MCState.expect`, `MCState.expect_and_grad`.
- `netket/vqs/full_summ/state.py` - `FullSumState`, `serialize_FullSumState`, `deserialize_FullSumState`.
- `netket/driver/vmc.py` - `VMC.compute_loss_and_update`, `VMC.energy`.
- `netket/_src/driver/vmc_sr.py` - `VMC_SR.compute_loss_and_update`, `get_forward_operator_VMCSR`.
- `netket/optimizer/sr.py` - `SR`, `check_conflicting_args_in_partial`.
- `netket/optimizer/solver/solvers.py` - `pinv_smooth`, `cholesky_with_fallback`, `solve`.
- `netket/logging/json_log.py` - `JsonLog.__call__`, `JsonLog.flush`.
- `netket/logging/state_log.py` - `StateLog.__call__`, `StateLog._save_variables`.
- `netket/_src/callbacks/save_state.py` - `SaveVariationalState` hooks.
- `netket/jax/_expect.py` - `expect`, `_expect_bwd` for custom differentiation path.

## Fast probes
- `rg -n "def expect|def expect_and_grad" netket/vqs/base.py netket/jax/_expect.py`
- `rg -n "class JsonLog|def flush" netket/logging/json_log.py`
- `rg -n "class SR|def check_conflicting_args_in_partial" netket/optimizer/sr.py`

## Validation checkpoints
- API behavior statements are backed by explicit callable symbols.
- Serialization/logging semantics are validated against logger/state functions.
