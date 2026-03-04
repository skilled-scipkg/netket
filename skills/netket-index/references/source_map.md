# netket source map: Index Router

Use this map only after routing with `doc_map.md` and the selected topic skill.

## Cross-topic function-level entry points
- `netket/tools/info.py` - `info`, `_jax_backends`: environment and backend diagnostics.
- `netket/vqs/mc/mc_state/state.py` - `MCState.__init__`, `MCState.sample`, `check_chunk_size`.
- `netket/driver/vmc.py` - `VMC.__init__`, `VMC.compute_loss_and_update`.
- `netket/_src/driver/vmc_sr.py` - `VMC_SR.compute_loss_and_update`.
- `netket/optimizer/sr.py` - `SR.lhs_constructor` and SR setup checks.
- `netket/jax/sharding/fixed_sharding_utils.py` - `distribute_to_devices_along_axis`, `gather`.

## Fast probes
- `rg -n "class VMC|def compute_loss_and_update" netket/driver/vmc.py netket/_src/driver/vmc_sr.py`
- `rg -n "def info|def _jax_backends" netket/tools/info.py`
- `rg -n "class MCState|def check_chunk_size" netket/vqs/mc/mc_state/state.py`

## Validation checkpoints
- Probe results map cleanly to one topic skill before deeper source exploration.
- Any implementation claim references a concrete symbol above.
