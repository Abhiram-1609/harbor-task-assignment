# Harbor task — JSON department salary totals

**A small [Harbor](https://github.com/laude-institute/harbor) benchmark task** for agent evaluation: read JSON employee records, compute total salary per department, and write a correctly formatted `output.json`.

If you are browsing this repo on GitHub, everything you need to understand and run the task is summarized here. Deeper file-level detail lives in the task folder linked below.

---

## About this repository

This project is a **single, self-contained Harbor task** (not the full Harbor framework). It was built for a **new-hire / assignment** style workflow: the task passes **Oracle** (reference solution) and **NOP** (no pre-baked success) checks, and is suitable to show in a portfolio or attach to a pull request against upstream Harbor.

**What “success” means for an agent**

- Input file: `/app/records.json` (array of `{ employee, department, salary }`).
- Output file: `/app/output.json` — object of `department → total salary`, keys **sorted A–Z**, **2-space** JSON indent, **newline** at end of file.

---

## Repository layout

```
harbor_tasks/json-dept-salary-totals/
├── task.toml           # Metadata, timeouts, CPU/RAM/disk
├── instruction.md      # Instructions shown to the agent
├── environment/        # Dockerfile + sample input only
├── solution/           # Reference solution (oracle)
└── tests/              # Verifier script + pytest tests
```

| Item | Value |
|------|--------|
| Task name (`task.toml`) | `harbor/json-dept-salary-totals` |
| Difficulty | easy |
| Category | data-processing |

More detail: **[`harbor_tasks/json-dept-salary-totals/README.md`](harbor_tasks/json-dept-salary-totals/README.md)**

---

## Who this is for

- **Reviewers / instructors** — quick sanity check of task structure and validation expectations.
- **You, running it locally** — clone this repo, clone Harbor, run `harbor run` pointing at `harbor_tasks/json-dept-salary-totals/`.
- **Contributors** — the same task may also be proposed via a fork/PR to [laude-institute/harbor](https://github.com/laude-institute/harbor) under `examples/tasks/` (naming may differ slightly, e.g. `test_state.py`).

---

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) (Docker Desktop on Windows is fine; WSL is often used with Harbor.)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- A clone of **[laude-institute/harbor](https://github.com/laude-institute/harbor)** and `uv sync` inside that repo so `uv run harbor …` works.

---

## Quick start (run the task)

In a terminal, from your **Harbor** clone (after `uv sync`):

```bash
# Replace TASK_PATH with the path to this repo’s task folder on your machine.
export TASK_PATH="/path/to/harbor-task-assignment/harbor_tasks/json-dept-salary-totals"

uv run harbor run --agent oracle --path "$TASK_PATH" --job-name oracle-json-dept
uv run harbor run --agent nop    --path "$TASK_PATH" --job-name nop-json-dept
```

**Expected results**

- **Oracle** — mean reward **1.0** (reference solution + tests pass).
- **NOP** — mean reward **0.0** (agent does nothing; output must not appear by default).

Lint the pytest file:

```bash
uvx ruff check "$TASK_PATH/tests/test_outputs.py"
```

On Windows PowerShell you can set the path instead:

```powershell
$TASK_PATH = "C:\Users\YOUR_USER\Desktop\HARBOR\harbor_tasks\json-dept-salary-totals"
cd C:\path\to\harbor-repo
uv run harbor run --agent oracle --path $TASK_PATH --job-name oracle-json-dept
```

---

## References

- [laude-institute/harbor](https://github.com/laude-institute/harbor) — framework and CLI
- Task format and concepts: see Harbor’s docs in that repository (e.g. `docs/` and `examples/tasks/`)

---

## License

Align with the license of the project you bundle or contribute this task with (for example, Harbor’s license when opening a PR upstream). This repo only adds task files and documentation.
