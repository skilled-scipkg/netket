# netket source map: Developer Guide

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/_src/driver/abstract_variational_driver.py` - `maybe_wrap_legacy_callback`, `AbstractVariationalDriver.run`, `apply_gradient`.
- `netket/_src/callbacks/base.py` - `AbstractCallback` hook methods (`on_step_start`, `on_compute_update_end`, `on_run_error`).
- `netket/jax/_expect.py` - `expect`, `_expect_fwd`, `_expect_bwd` dispatch internals.
- `netket/vqs/base.py` - public expectation dispatch (`expect`, `expect_and_grad`).
- `netket/vqs/mc/mc_state/expect.py` - `get_local_kernel`, `_expect`, `expect`.
- `netket/vqs/full_summ/expect.py` - `expect_and_grad_fullsum`, `expect_and_forces_fullsum`.
- `netket/_src/vqs/expect_to_precision.py` - `expect_to_precision` adaptive-evaluation loop.

## Fast probes
- `rg -n "def maybe_wrap_legacy_callback|def run" netket/_src/driver/abstract_variational_driver.py`
- `rg -n "def expect|def _expect_bwd" netket/jax/_expect.py netket/vqs/base.py`
- `rg -n "class AbstractCallback|def on_" netket/_src/callbacks/base.py`

## Validation checkpoints
- Developer guidance references exact extension hooks.
- Behavior changes are testable by targeting the symbols listed above.
