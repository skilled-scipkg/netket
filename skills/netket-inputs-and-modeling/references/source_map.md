# netket source map: Inputs and Modeling

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/hilbert/spin.py` - `_check_total_sz`, `Spin`.
- `netket/hilbert/fock.py` - `Fock`.
- `netket/hilbert/index/constrained_sum.py` - `optimalConstrainedHilbertindex`, `SumConstrainedHilbertIndex`.
- `netket/operator/_graph_operator.py` - `GraphOperator`, `check_acting_on_subspace`.
- `netket/operator/_ising/jax.py` - `IsingJax`, `_ising_kernel_jax`.
- `netket/operator/_fermion2nd/utils.py` - `_canonicalize_input`, `_verify_input`, `_normal_ordering`.
- `netket/models/rbm.py` - `RBM`, `RBMSymm`.
- `netket/models/tensor_networks/mps.py` - `MPSPeriodic`, `MPSOpen`.
- `netket/sampler/metropolis.py` - `MetropolisSampler`, `MetropolisLocal`, `MetropolisExchange`.
- `netket/sampler/rules/local.py` - `LocalRule`.
- `netket/sampler/rules/exchange.py` - `ExchangeRule`, `compute_clusters`.
- `netket/vqs/mc/mc_state/state.py` - `MCState.__init__`, `MCState.sample`, `check_chunk_size`.

## Fast probes
- `rg -n "class Spin|class Fock|class SumConstrainedHilbertIndex" netket/hilbert`
- `rg -n "def GraphOperator|class RBM|def MetropolisExchange" netket/operator netket/models netket/sampler`
- `rg -n "class MCState|def sample|def check_chunk_size" netket/vqs/mc/mc_state/state.py`

## Validation checkpoints
- Incompatible graph/hilbert/operator combinations are checked at constructor-level.
- Sampler/state shape semantics are validated via the listed state/sampler functions.
