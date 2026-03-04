# netket source map: Theory and Methods

Use this map only after exhausting docs in `doc_map.md`.

## Function-level entry points
- `netket/_src/symmetry/representation_construction.py` - `physical_to_logical_permutation_group`.
- `netket/_src/symmetry/canonical_representation.py` - `canonical_representation`.
- `netket/_src/symmetry/representation.py` - `Representation` core object.
- `netket/nn/blocks/symmetry_sum.py` - `SymmExpSum` symmetry-aware neural block.
- `netket/operator/_abstract_super_operator.py` - `AbstractSuperOperator` interface.
- `netket/operator/_local_liouvillian.py` - `LocalLiouvillian` Lindblad implementation surface.
- `netket/hilbert/doubled_hilbert.py` - `DoubledHilbert` for density-matrix formulations.
- `netket/vqs/full_summ/expect.py` - `expect`, `expect_and_grad_fullsum`, `expect_and_forces_fullsum`.
- `netket/experimental/observable/renyi2/expect.py` - `Renyi2`, `Renyi2_sampling_MCState`.
- `netket/experimental/observable/variance/expect.py` - `expect`, `expect_and_grad`.

## Fast probes
- `rg -n "def canonical_representation|class Representation" netket/_src/symmetry`
- `rg -n "class LocalLiouvillian|class AbstractSuperOperator" netket/operator`
- `rg -n "def expect_and_grad_fullsum|def Renyi2" netket/vqs/full_summ/expect.py netket/experimental/observable/renyi2/expect.py`

## Validation checkpoints
- Theory-driven answers reference specific representation/superoperator/expectation implementations.
- Method claims can be checked via callable functions above on small systems.
