# netket source map: User Guides

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/optimizer/sr.py` - `check_conflicting_args_in_partial`, `SR.lhs_constructor`.
- `netket/optimizer/qgt/default.py` - `default_qgt_matrix`, `QGTAuto.__call__`.
- `netket/optimizer/solver/solvers.py` - `pinv_smooth`, `cholesky_with_fallback`, `solve`.
- `netket/driver/vmc.py` - `VMC.compute_loss_and_update`, `VMC.preconditioner`.
- `netket/_src/driver/vmc_sr.py` - `VMC_SR.compute_loss_and_update`, `mode` property behavior.
- `netket/operator/_local_operator/jax.py` - `LocalOperatorJax`, `_local_operator_kernel_jax`.
- `netket/operator/_fermion2nd/utils.py` - `_canonicalize_input`, `_verify_input`.
- `netket/vqs/base.py` - `expect`, `expect_and_grad`.
- `netket/vqs/mc/mc_state/state.py` - `quantum_geometric_tensor`, `check_mc_convergence`.
- `netket/utils/history/accum.py` - `accum_histories`, `accum_histories_in_tree`.

## Fast probes
- `rg -n "class SR|def default_qgt_matrix|def pinv_smooth" netket/optimizer`
- `rg -n "def quantum_geometric_tensor|def check_mc_convergence" netket/vqs/mc/mc_state/state.py`
- `rg -n "def _canonicalize_input|class LocalOperatorJax" netket/operator`

## Validation checkpoints
- User-guide recommendations map to explicit optimizer/driver/operator/state functions.
- Numerical stability guidance is traceable to SR/QGT solver implementations.
