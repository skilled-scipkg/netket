# netket documentation map: Parallel and HPC

## Distributed execution docs
- `docs/parallel.md` - overall parallel mode selection.
- `docs/parallel-multigpu.md` - single-node multi-GPU basics.
- `docs/parallel-multinode.md` - multi-node setup and launcher constraints.
- `docs/parallel-mpi.md` - MPI backend path and caveats.
- `docs/distributed-computing.md` - redirect context and distributed notes.
- `docs/sharp-bits.md` - runtime/deadlock/platform pitfalls.
- `test_sharding/readme.md` - sharding test script entry points.
- `Examples/Sharding/multi_process.py` - practical distributed script pattern.

## Startup commands
```bash
djaxrun --simple -np 2 python Examples/Sharding/multi_process.py
python -c 'import jax; jax.distributed.initialize(); print(jax.process_index(), jax.process_count())'
```

## Validation checkpoints
- Every rank prints consistent process index/count.
- Local and global device counts match scheduler allocation.
- Small distributed smoke run succeeds before large jobs.
