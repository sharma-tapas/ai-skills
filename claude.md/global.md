# Global Development Guardrails

Rules that apply to every session in this repository, regardless of the current task.

---

## Guardrails

### What Claude Must Always Do

- Read `claude.md/architecture.rules` before generating any Go or Python code.
- Read `claude.md/project.md` before making any assumption about project-specific configuration, naming, or dependencies.
- Regenerate gRPC stubs (`buf generate`) after any `.proto` change before writing application code that uses the new types.
- Add a matching `<project>ctl` CLI command for every new gRPC/REST endpoint.
- Keep the three architecture layers strictly separate — never import across the boundary in the wrong direction.

### What Claude Must Never Do

- Write hand-rolled HTTP handlers in Go — all REST is generated via grpc-gateway.
- Edit files under `gen/` — they are machine-generated from `proto/`.
- Add application logic to `cmd/` or CLI command files — only wiring lives there.
- Use `viper.Get*` inside a Cobra command's `init()` function.
- Add a `// TODO` or `// FIXME` without also creating a task to address it in the same session.
- Commit or suggest committing generated files without running `buf generate` and `buf lint` first.
- Mix unit and integration test fixtures in the same `conftest.py`.
- Skip type annotations on any new Python function signature.

### Scope Discipline

- Fix the reported bug — do not refactor surrounding code unless directly related.
- Do not add abstraction layers, helper utilities, or new packages that are not required by the current task.
- Do not introduce feature flags, backwards-compatibility shims, or optional parameters for hypothetical future use.

---

## Ralph Loop — Iterative Development Workflow

Use `/ralph-loop` for well-defined, iterative tasks where Claude should self-correct across multiple passes (greenfield features, test coverage gaps, refactors with clear end state).

### Starting a Loop

```
/ralph-loop "<clear task description>" --completion-promise "<PROMISE_TEXT>" --max-iterations <n>
```

**Example — implement a new gRPC endpoint end-to-end:**
```
/ralph-loop "Implement the CreateOrder RPC: update proto, regenerate stubs, write domain entity, use case, infra repo, wire into server, add orderctl create command, write unit tests. Output <promise>CREATE ORDER COMPLETE</promise> when all tests pass and buf lint is clean." --completion-promise "CREATE ORDER COMPLETE" --max-iterations 15
```

### Loop Prompt Requirements

A good ralph loop prompt for this codebase must include:

| Element | Example |
|---|---|
| Layer scope | "update proto, regenerate stubs, write use case, write infra repo" |
| CLI requirement | "add `<project>ctl <cmd>` command" |
| Test requirement | "unit tests for use case, integration test for repo" |
| Completion signal | `Output <promise>DONE</promise> when all tests pass` |
| Verification step | "run `go test ./...` and `buf lint` before signalling completion" |

### Completion Signal

Claude must emit this exact tag when the task is done and verified:

```
<promise>TASK COMPLETE</promise>
```

Without this tag (or `--max-iterations`), the loop runs indefinitely.

### When NOT to Use Ralph Loop

- Debugging a production incident — use targeted `systematic-debugging` instead.
- Tasks requiring a design decision or human input mid-way.
- One-shot queries or explanations.
- Any task where the success criteria cannot be verified programmatically (tests passing, lint clean, etc.).

### Cancelling a Loop

```
/cancel-ralph
```

This removes the loop state file and stops the next iteration.
