---
name: netket-theory-and-methods
description: This skill should be used when users ask about theory and methods in netket; it prioritizes documentation references and then source inspection only for unresolved details.
---

# netket: Theory and Methods

## High-Signal Playbook
### Route conditions
- Route to `netket-user-guides` for practical module usage and parameter defaults.
- Route to `netket-simulation-workflows` for run-loop and convergence operations.
- Route to `netket-inputs-and-modeling` for concrete Hilbert/operator/model construction.

### Triage questions
- Is the question about symmetry representations, SR/QGT geometry, or open-system (Lindblad) methods?
- Does the user need a derivation-level explanation or runnable implementation checks?
- Is there a small exact baseline available for comparison?

### Canonical workflow
1. Start from the closest theory doc in `Primary documentation references`.
2. Translate theoretical objects into explicit NetKet objects (Hilbert, operator, vstate, driver).
3. Run a small-system sanity simulation before large-scale runs.
4. Compare observables against expected invariants or exact/full-summation baselines.
5. Escalate to `references/source_map.md` for algorithm-level behavior checks.

### Minimal operational checks
```bash
python Examples/FullSummation/ising.py
python Examples/DissipativeIsing1d/ising1d.py
```

### Validation checkpoints
- Symmetry constraints and representations are consistent with model output.
- Superoperator/Lindblad runs produce finite, interpretable observables.
- Small-system baselines agree with theoretical expectations.

## Scope
- Handle theoretical and algorithmic-method questions.
- Bridge docs-level theory to runnable simulation decisions.

## Primary documentation references
- `docs/advanced/symmetry.md`
- `docs/user-guides/superop.md`
- `docs/user-guides/sr.md`
- `docs/vmc-from-scratch/index.md`

## Workflow
- Start docs-first for definitions and assumptions.
- Use `references/doc_map.md` to expand across related method docs.
- Use `references/source_map.md` only for implementation-specific behavior.

## Tutorials and examples
- `docs/tutorials`
- `Examples/FullSummation/ising.py`
- `Examples/DissipativeIsing1d/ising1d.py`

## Test references
- `test/observable`
- `test/operator`
- `test/variational`

## Optional deeper inspection
- `netket`

## Source entry points for unresolved issues
- `netket/_src/symmetry/representation_construction.py` (`physical_to_logical_permutation_group`)
- `netket/_src/symmetry/canonical_representation.py` (`canonical_representation`)
- `netket/_src/symmetry/representation.py` (`Representation`)
- `netket/nn/blocks/symmetry_sum.py` (`SymmExpSum`)
- `netket/operator/_local_liouvillian.py` (`LocalLiouvillian`)
- `netket/operator/_abstract_super_operator.py` (`AbstractSuperOperator`)
- `netket/hilbert/doubled_hilbert.py` (`DoubledHilbert`)
- Prefer targeted source search: `rg -n "<symbol_or_keyword>" netket`
