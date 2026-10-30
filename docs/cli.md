# Command Line

After [building the native solver](installation.md#command-line-executable), run:

```bash
mkdir -p output
./build/pdhcg problem.qps output
```

The first argument is an MPS, QPS, or CBF file; gzip-compressed variants are also
accepted. The second is an existing output directory.

For `problem.qps`, the output files are:

| File | Contents |
| --- | --- |
| `problem_summary.txt` | Termination status, objectives, residuals, and timing |
| `problem_primal_solution.txt` | Primal solution, one value per line |
| `problem_dual_solution.txt` | Dual solution, one value per line |

## Solver options

For example, set a time limit and tighter tolerances:

```bash
./build/pdhcg problem.qps output --time_limit 60 --eps_opt 1e-6 --eps_feas 1e-6
```

The executable's help lists all supported flags, accepted values, and defaults:

```bash
./build/pdhcg --help
```

See [Devices](devices.md) for backend selection, CPU threads, and multi-GPU
execution; see [Algorithm](algorithm.md) for the solver's update and certificate
conditions.

## Quadratic update options

`--k_p <value>` sets the finite, nonnegative proportional gain of the primal
weight controller. `--linearized 1` selects linearized quadratic updates;
`--linearized 0` selects inner updates. It is an alias for
`--non_diagonal_quadratic_mode`; the last supplied option takes precedence.

The summary's `Read Time (sec)` measures input reading and parsing.
`Runtime (sec)` measures solver iterations, excluding reading, QCQP lifting,
rescaling and initialization.
