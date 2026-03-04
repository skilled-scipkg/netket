# netket documentation map: Simulation Workflows

## Simulation run-loop docs
- `docs/user-guides/drivers.md` - driver construction and run flow.
- `docs/user-guides/varstate.md` - state setup and sampling controls.
- `docs/user-guides/sampler.ipynb` - sampler behavior and acceptance intuition.
- `docs/user-guides/sr.md` - SR/QGT regularization and schedules.
- `docs/api/drivers.md` - driver API signatures.
- `docs/api/optimizer.md` - optimizer/preconditioner APIs.
- `docs/api/logging.md` - logging backends and persistence options.
- `docs/api/callbacks.md` - callback interfaces and built-ins.
- `docs/advanced/custom_callbacks.md` - hook-level callback lifecycle.
- `docs/sharp-bits.md` - numerical/runtime pitfalls.

## Baseline run command
```bash
python Examples/Heisenberg1d/heisenberg1d.py
```

## Validation checkpoints
- Energy/error traces are finite and improve over iterations.
- Acceptance and effective sample settings are monitored.
- JSON/state outputs exist and can be resumed from.
