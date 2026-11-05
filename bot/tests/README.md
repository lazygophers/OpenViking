# VikingBot tests

All Bot tests live in this directory, including provider and OpenViking session
tests previously under `vikingbot/tests/unit`.

From the repository root, with the bot and dev dependencies installed:

```sh
bash bot/scripts/test_all.sh -q
```

The runner uses the repository `.venv` without syncing dependencies. Set
`VIKINGBOT_TEST_PYTHON` to use another Python environment. Pytest arguments are
forwarded, for example `-k streaming` or `--cov=vikingbot`.

Keep tests of observable behavior on active paths: agent/tool execution,
streaming and provider failover, authentication and session isolation, memory
recall/commit, sandbox boundaries, channel delivery, and Compile task lifecycle.
Use real package imports and pytest-managed temporary directories. Mock external
services at their boundaries; do not replace package modules to bypass imports.
Parameterize cases that exercise the same path and assertions, and share setup
for persisted sessions instead of copying JSONL fixtures across tests.
Assert observable results rather than internal call avoidance, object identity,
or unrelated behavior staying unchanged after a feature change. Keep negative
checks that protect authorization, data integrity, and duplicate delivery.

Enable the feature being tested before asserting that it rejects or skips work;
otherwise an early return can make the test pass for the wrong reason. Check
persisted state with a fresh reader. Budget and concurrency tests should also
prove that useful work completed, and recovery tests should reach a successful
retry. Keep each test focused on one behavior, with explicit expected results.

## Environment gotchas

- Standard entry points are `make test` and `make lint` from the repository
  root; they sync the required extras and run the suite and lint checks.

- Worktree test runs: build the editable install serially. `uv.lock` pins the
  openviking source path to the worktree where the environment was created;
  parallel `uv sync` across worktrees fail both builds (cross-locked) and
  contend on uv's editable build lock (300s timeout).
- Run bot tests in a worktree with:
  `cd bot && OV_SKIP_CPP_BUILD=1 uv run --extra test pytest <files>`.
  `--extra test` is required: pytest-asyncio lives in the `test` extra, and the
  default sync omits it. `OV_SKIP_CPP_BUILD=1` skips the C++ engine build,
  which bot tests do not need.
- The main-workspace `.venv` also lacks pytest-asyncio by default; install it
  there (`uv pip install pytest-asyncio`) before running the suite from the
  main tree.
