# netket source map: Simulation Workflows

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/driver/vmc.py` - `VMC.compute_loss_and_update`, `VMC.energy`.
- `netket/_src/driver/vmc_sr.py` - `VMC_SRt`, `VMC_SR.compute_loss_and_update`.
- `netket/_src/driver/abstract_variational_driver.py` - `AbstractVariationalDriver.run`, `estimate`, `apply_gradient`.
- `netket/vqs/mc/mc_state/state.py` - `MCState.expect_and_grad`, `MCState.check_mc_convergence`, `expect_to_precision`.
- `netket/optimizer/sr.py` - `SR.lhs_constructor`.
- `netket/optimizer/qgt/default.py` - `default_qgt_matrix`, `QGTAuto.__call__`.
- `netket/logging/json_log.py` - `JsonLog._flush_log`, `JsonLog.flush`.
- `netket/logging/state_log.py` - `StateLog.__call__`, `StateLog._save_variables`.
- `netket/_src/callbacks/base.py` - callback hook stages and stop logic.
- `netket/_src/callbacks/save_state.py` - checkpoint callback behavior.
- `netket/callbacks/invalid_loss_stopping.py` - invalid-loss early stop.
- `netket/callbacks/timeout.py` - timeout-based early stop.

## Fast probes
- `rg -n "def compute_loss_and_update|def run" netket/driver/vmc.py netket/_src/driver/vmc_sr.py netket/_src/driver/abstract_variational_driver.py`
- `rg -n "def expect_to_precision|def check_mc_convergence" netket/vqs/mc/mc_state/state.py`
- `rg -n "class JsonLog|class StateLog|class SaveVariationalState" netket/logging netket/_src/callbacks/save_state.py`

## Validation checkpoints
- Convergence/runtime claims are tied to driver/state/logger callback functions above.
- Callback and checkpoint behavior is validated at hook-level, not only by output files.
