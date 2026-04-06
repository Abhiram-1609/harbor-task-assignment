# Harbor task: JSON department salary totals

This repository contains a **Harbor** benchmark task: read employee records from JSON, aggregate salaries by department, and write a deterministic `output.json`.

## What’s inside

| Path | Description |
|------|-------------|
| [`harbor_tasks/json-dept-salary-totals/`](harbor_tasks/json-dept-salary-totals/) | Full task: `instruction.md`, `task.toml`, `environment/`, `solution/`, `tests/` |
| [`harbor_tasks/json-dept-salary-totals/README.md`](harbor_tasks/json-dept-salary-totals/README.md) | Task-specific details, I/O spec, and run commands |

**Task package name:** `harbor/json-dept-salary-totals`  
**Difficulty:** easy · **Category:** data-processing

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- A local clone of [laude-institute/harbor](https://github.com/laude-institute/harbor) (to run the `harbor` CLI)

## Run the task

From your Harbor clone (after `uv sync`), use the **absolute or relative path** to this task on your machine:

```bash
cd /path/to/harbor
uv run harbor run --agent oracle --path /path/to/this/repo/harbor_tasks/json-dept-salary-totals --job-name oracle
uv run harbor run --agent nop    --path /path/to/this/repo/harbor_tasks/json-dept-salary-totals --job-name nop
```

**Expect:** Oracle mean reward **1.0**, NOP mean reward **0.0**.

Lint:

```bash
uvx ruff check /path/to/this/repo/harbor_tasks/json-dept-salary-totals/tests/test_outputs.py
```

## Upstream contribution

An equivalent example task lives under **`examples/tasks/json-dept-salary-totals/`** in a fork of Harbor for pull requests to [laude-institute/harbor](https://github.com/laude-institute/harbor). This repo keeps the assignment layout (`harbor_tasks/`, `test_outputs.py`) in one place.

## References

- [Harbor repository](https://github.com/laude-institute/harbor)
- [Harbor task documentation](https://harborframework.com/docs/tasks) (if published for your Harbor version)

## License

Unless noted otherwise, follow the license of the parent project you bundle this task with (e.g. Harbor’s license when contributing upstream).
