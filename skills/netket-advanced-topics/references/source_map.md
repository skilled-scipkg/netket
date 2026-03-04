# netket source map: Advanced Topics

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/_src/driver/abstract_variational_driver.py` - `AbstractVariationalDriver.run`, `maybe_wrap_legacy_callback`.
- `netket/driver/vmc.py` - `VMC.compute_loss_and_update`, `get_forward_operator_VMC`.
- `netket/_src/driver/vmc_sr.py` - `VMC_SRt`, `VMC_SR.compute_loss_and_update`.
- `netket/_src/callbacks/save_state.py` - `SaveVariationalState.before_parameter_update`, `_nqxpack_save`.
- `netket/jax/sharding/fixed_sharding_utils.py` - `distribute_to_devices_along_axis`, `shard_along_axis`, `gather`.
- `netket/utils/struct/pytree_serialization_sharding.py` - `from_flax_state_dict_sharding_strict`, `from_flax_state_dict_sharding_relaxed`.
- `netket/_src/callbacks/auto_slurm_requeue.py` - `get_time_left`, `is_requeueable`, `AutoSlurmRequeue`.

## Fast probes
- `rg -n "def run|def maybe_wrap_legacy_callback" netket/_src/driver/abstract_variational_driver.py`
- `rg -n "class VMC_SR|def VMC_SRt" netket/_src/driver/vmc_sr.py`
- `rg -n "def distribute_to_devices_along_axis|def gather" netket/jax/sharding/fixed_sharding_utils.py`

## Validation checkpoints
- Advanced behavior questions are answered with specific function/class references.
- Sharding/checkpoint claims can be traced to the symbols listed above.
