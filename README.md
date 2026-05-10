# tapas-claude-toolkit

A curated Claude Code plugin providing skills for professional software engineering workflows. The toolkit covers test-driven development, idiomatic Go and Python patterns, design challenge interviews, Jira integration, PRD authoring, and production guardrails — built around clean architecture and disciplined feature development.

---

## Installation

```bash
claude plugin add /path/to/ai-skills
```

Or reference the directory directly in your Claude Code project settings.

---

## Skills

The plugin ships **11 skills**. Each skill is automatically invoked by Claude when the context matches its trigger conditions — no manual activation needed beyond describing what you want.

### `tdd-workflow`

**Trigger phrases**: "write tests", "TDD", "test-driven", "RED-GREEN-REFACTOR", "tracer bullet", "implement with tests", fixing bugs, refactoring

Enforces vertical-slice TDD: one test written, one implementation to make it pass, repeat. Prevents the "horizontal slicing" anti-pattern of writing all tests first then all implementation, which produces tests that verify imagined behavior rather than real outcomes.

Key guarantees:
- RED gate: a test must be compiled and executed (not just written) before implementation starts
- GREEN gate: tests must pass before refactoring begins
- Git checkpoint commits at each stage (RED commit, GREEN commit, refactor commit)
- 80%+ coverage as a result of behavior testing, not a target in itself

Reference files bundled with the skill: `tests.md` (good/bad test examples), `mocking.md` (when and what to mock), `deep-modules.md`, `interface-design.md`, `refactoring.md`.

---

### `golang-patterns`

**Trigger phrases**: writing Go code, Go idioms, Go best practices, structuring Go services, error handling in Go

Idiomatic Go patterns for building robust, efficient, maintainable applications. Covers:
- Error wrapping and sentinel errors
- Interface design at the point of use
- Clean architecture layer separation (`domain/` → `usecase/` → `infra/`)
- Constructor patterns, dependency injection
- Context propagation, concurrency patterns
- gRPC + grpc-gateway service structure

---

### `golang-testing`

**Trigger phrases**: Go tests, table-driven tests, Go benchmarks, Go fuzzing, testing Go code, Go test coverage

Comprehensive Go testing patterns following TDD methodology:
- Table-driven tests with `t.Run` subtests
- Benchmark writing and profiling
- Fuzz testing with `testing.F`
- Interface mocking without third-party libraries
- Integration test patterns with real DB/external deps
- Coverage reporting and threshold enforcement

---

### `python-patterns`

**Trigger phrases**: writing Python, Python idioms, Pythonic code, Python best practices, Python type hints, PEP 8

Idiomatic Python patterns for production-quality applications:
- PEP 8 style and Google Style Guide docstrings
- Type annotations on all function signatures (strict mypy)
- `dataclasses` and `pydantic.BaseModel` for value objects
- Protocol-based abstractions in `usecase/`
- Clean architecture: `domain/` → `usecase/` → `infra/` → `entrypoints/`
- `uv` + `ruff` + `mypy` toolchain usage

---

### `python-testing`

**Trigger phrases**: pytest, Python testing, Python fixtures, parametrize, Python mocking, Python coverage

Testing strategies for Python using pytest:
- Fixture design in `conftest.py`
- `@pytest.mark.parametrize` for table-driven tests
- `unittest.mock` and `pytest-mock` patterns
- Integration test isolation with `@pytest.mark.integration`
- Coverage configuration in `pyproject.toml`
- Excluding integration tests from default `pytest` runs

---

### `grill-me`

**Trigger phrases**: "grill me", "challenge my plan", "poke holes in this", "stress test my design", "what am I missing", pre-implementation design review

A relentless design interviewer. Given a plan or spec in the current conversation, it walks the design through a full decision tree — challenging every architectural choice, data model decision, deployment assumption, and edge case before a single line of implementation is written.

Context-aware: reads `architecture.rules` from the project and any brainstorming output in the session, then challenges every decision against that context. Produces a refined plan with open questions resolved.

Part of the three-step feature development workflow:
1. `/brainstorming` — rough plan
2. `/grill-me` — challenge and sharpen
3. `/to-prd` — structured PRD

---

### `to-prd`

**Trigger phrases**: "create a PRD", "write a PRD", "turn this into a PRD", "publish requirements", converting a plan to requirements

Synthesizes the current conversation context and codebase understanding into a structured Product Requirements Document. Does not re-interview the user — uses what is already known.

Publishes the PRD to the project issue tracker. Requires issue tracker and triage label vocabulary to be configured (see `claude.md/project.md`).

PRDs are written to `docs/prd/<feature>-prd.md`. Per the project workflow, no implementation may start without a PRD in place.

---

### `to-issues`

**Trigger phrases**: "break into issues", "create tickets", "split into tasks", "make GitHub issues from this plan", converting a plan to an issue tracker

Converts a plan, spec, or PRD into independently-grabbable issues using tracer-bullet vertical slices. Each issue is self-contained and implementable without depending on other issues being done first.

Follows the project's triage label vocabulary and issue format conventions.

---

### `jira-integration`

**Trigger phrases**: Jira tickets, retrieve Jira issues, update Jira status, add Jira comments, transition issues, Jira MCP, Jira REST API

Provides Jira workflow patterns via MCP (preferred) or direct REST API fallback:
- Fetch issues by JQL query
- Update ticket status, assignee, labels
- Add comments with structured output
- Transition issues through workflow states
- Link pull requests to tickets

Supports both `mcp__plugin_atlassian_atlassian__*` tool calls (when the Atlassian MCP is connected) and `curl`-based REST calls when MCP is unavailable.

---

### `guardrails`

**Trigger phrases**: production systems, running agents autonomously, destructive operations, safeguards, prevent data loss

Prevents destructive operations when working on production systems or running Claude agents autonomously. Enforces explicit confirmation before:
- Dropping databases, tables, or indexes
- Deleting files outside designated scratch directories
- Force-pushing to protected branches
- Stopping or restarting production processes
- Applying migrations to live environments without a dry-run first

Use whenever deploying agents in unattended or semi-attended mode against real infrastructure.

---

### `team-builder`

**Trigger phrases**: "build a team", "parallel agents", "dispatch agents", "compose a team", spinning up multiple agents for a task

Interactive menu for browsing and composing parallel agent teams. Presents available agents (flat or domain-organized) and lets you pick a combination to dispatch concurrently for a task.

Useful when a feature spans multiple domains (e.g., backend + frontend + infra) and the work can be parallelized across specialized agents.

---

## Project Configuration

The `claude.md/` directory contains project-level rules loaded automatically by Claude Code:

| File | Purpose |
|---|---|
| `claude.md/global.md` | Guardrails that apply to every session: what Claude must always/never do, Ralph Loop workflow |
| `claude.md/project.md` | Project identity, repo layout, environment variables, key commands, Prometheus metrics requirements |
| `claude.md/architecture.rules` | Clean architecture layer rules for Go and Python, gRPC/REST gateway conventions, CLI (`<project>ctl`) patterns, code quality standards |

These files are read by Claude before generating any code and take precedence over default behavior.

---

## Feature Development Workflow

The toolkit is designed around a three-step planning sequence before implementation:

```
1. /brainstorming --model haiku   → rough plan (cheap, fast)
2. /grill-me                      → challenge assumptions, resolve blind spots
3. /to-prd                        → structured PRD to docs/prd/<feature>-prd.md
```

No implementation task (proto changes, use case code, CLI command) starts without a PRD. Ralph Loop prompts reference the PRD as the completion criteria source of truth.

---

## Directory Structure

```
ai-skills/
├── .claude-plugin/
│   └── plugin.json               # Plugin manifest
├── claude.md/
│   ├── architecture.rules        # Go + Python architecture rules
│   ├── global.md                 # Session-wide guardrails and Ralph Loop docs
│   └── project.md                # Project identity, commands, dependencies
├── skills/
│   ├── golang-patterns/
│   │   └── SKILL.md
│   ├── golang-testing/
│   │   └── SKILL.md
│   ├── grill-me/
│   │   └── SKILL.md
│   ├── guardrails/
│   │   └── SKILL.md
│   ├── jira/
│   │   └── SKILL.md
│   ├── python-patterns/
│   │   └── SKILL.md
│   ├── python-testing/
│   │   └── SKILL.md
│   ├── tdd/
│   │   ├── SKILL.md
│   │   ├── deep-modules.md       # Deep module design reference
│   │   ├── interface-design.md   # Interface design for testability
│   │   ├── mocking.md            # Mocking guidelines
│   │   ├── refactoring.md        # Refactor patterns
│   │   └── tests.md              # Good vs bad test examples
│   ├── team-builder/
│   │   └── SKILL.md
│   ├── to-issues/
│   │   └── SKILL.md
│   └── to-prd/
│       └── SKILL.md
└── README.md
```

---

## Philosophy

These skills embody three principles:

**Behavior over implementation.** Tests verify what the system does through public interfaces, not how it does it internally. Code can change; tests shouldn't need to.

**Vertical slices over horizontal layers.** Features are built as end-to-end tracer bullets (one test → one implementation → repeat), not by writing all tests first and all implementations second. This keeps feedback tight and tests grounded in reality.

**Plan before code.** Non-trivial features go through brainstorm → challenge → PRD before implementation begins. This catches design errors when they're cheap to fix, not after the code is written.

---

## License

MIT
