# netket source map: Examples and Tutorials

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/driver/vmc.py` - `VMC.compute_loss_and_update` (used by baseline examples).
- `netket/_src/driver/vmc_sr.py` - `VMC_SR.compute_loss_and_update` (SR/minSR examples).
- `netket/sampler/metropolis.py` - `MetropolisLocal`, `MetropolisExchange`, `MetropolisSampler`.
- `netket/models/rbm.py` - `RBM`, `RBMSymm` classes used in many examples.
- `netket/models/autoreg.py` - `ARNNSequential`, `ARNNDense`, autoregressive flow.
- `netket/vqs/mc/mc_state/state.py` - `MCState.sample`, `MCState.expect`.
- `netket/jax/sharding/fixed_sharding_utils.py` - `distribute_to_devices_along_axis`, `gather` for sharding demos.
- `netket/experimental/observable/infidelity/expect.py` - `infidelity` for fidelity/infidelity tutorials.

## Fast probes
- `rg -n "nk\.driver|nk\.vqs|nk\.sampler" Examples/Ising1d/ising1d.py Examples/Heisenberg1d/heisenberg1d.py`
- `rg -n "class RBM|class ARNNDense|def MetropolisExchange" netket/models/rbm.py netket/models/autoreg.py netket/sampler/metropolis.py`

## Validation checkpoints
- Tutorial behavior can be traced from example script calls to concrete NetKet functions.
- Divergences are checked at function-level, not only at high-level script output.
