# json-dept-salary-totals

Harbor example task: aggregate employee salaries by department from a JSON file and write a deterministic JSON report.

## Objective

The agent (or reference solution) must:

1. Read **`/app/records.json`** — a JSON array of objects with `employee`, `department`, and `salary` (integer).
2. Sum **`salary`** for each **`department`**.
3. Write **`/app/output.json`** — a JSON object mapping department name → total salary, with:
   - keys sorted **alphabetically**;
   - **2-space** indentation;
   - a **single trailing newline** after the closing `}`.

## Layout

```text
json-dept-salary-totals/
├── task.toml              # Task metadata and resource limits
├── instruction.md         # Agent-facing instructions
├── environment/
│   ├── Dockerfile         # Image + input data only (no tests/solution)
│   └── records.json       # Sample input
├── solution/
│   └── solve.sh           # Reference solution (computes from input)
└── tests/
    ├── test.sh            # Verifier: uvx + pytest + reward file
    └── test_outputs.py    # Pytest cases (assignment layout)
```

In the upstream Harbor repo copy, the pytest file is named **`test_state.py`** to match other examples; behavior is the same.

## Input format (`records.json`)

Example shape:

```json
[
  {"employee": "Alice", "department": "Engineering", "salary": 95000},
  {"employee": "Bob", "department": "Sales", "salary": 72000}
]
```

## Expected output (`output.json`)

For the bundled `records.json`, totals are:

- `Engineering` → `200000`
- `HR` → `68000`
- `Sales` → `160000`

Keys appear in order: **Engineering**, **HR**, **Sales**.

## Run locally

From a checkout of [Harbor](https://github.com/laude-institute/harbor) with `uv sync` applied, point `harbor run` at this directory (adjust the path):

```bash
# Reference solution / verifier (expect mean reward 1.0)
uv run harbor run --agent oracle --path path/to/json-dept-salary-totals --job-name oracle-json-dept

# NOP agent (expect mean reward 0.0 — output must not exist beforehand)
uv run harbor run --agent nop --path path/to/json-dept-salary-totals --job-name nop-json-dept
```

Lint tests:

```bash
uvx ruff check path/to/json-dept-salary-totals/tests/test_outputs.py
# or test_state.py in the examples/ copy
```

## Metadata

| Field        | Value              |
|-------------|--------------------|
| Difficulty  | easy               |
| Category    | data-processing    |
| Package name| `harbor/json-dept-salary-totals` |

Update **`task.toml`** `[metadata]` / `[task]` authors if you fork this for your own submission.

## License

Follow the license of the repository this task lives in (e.g. Harbor upstream or your fork).
