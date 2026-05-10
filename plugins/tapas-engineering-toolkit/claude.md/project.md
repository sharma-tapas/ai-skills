# Project Configuration

Fill this file in when a project is initialised in this workspace. Future Claude sessions will read it before writing any code.

---

## Project Identity

```
Project name:      <project>          # e.g. "auth", "order", "inventory"
CLI binary name:   <project>ctl       # e.g. "authctl"
Go module path:    github.com/<org>/<project>
Python package:    <project>          # src/<project>/
Proto package:     <org>.<project>.v1
```

## Repository Layout

```
.
├── proto/                    # .proto source files
├── gen/go/                   # generated Go stubs (buf generate)
├── gen/openapiv2/            # generated Swagger docs
├── internal/
│   ├── domain/
│   ├── usecase/
│   └── infra/
├── cmd/
│   ├── server/               # gRPC + REST gateway entrypoint
│   └── <project>ctl/         # CLI entrypoint
├── src/<project>/            # Python service (if present)
│   ├── domain/
│   ├── usecase/
│   ├── infra/
│   └── entrypoints/
├── tests/
│   ├── unit/
│   └── integration/
├── buf.yaml
├── buf.gen.yaml
├── go.mod
├── pyproject.toml            # Python deps + tool config
└── uv.lock
```

## Environment Variables

| Variable | Description | Required |
|---|---|---|
| `<PROJECT>_GRPC_PORT` | gRPC server listen port (default 50051) | Yes |
| `<PROJECT>_HTTP_PORT` | REST gateway listen port (default 8080) | Yes |
| `<PROJECT>_DB_DSN` | Database connection string | Yes |
| `<PROJECT>_LOG_LEVEL` | Log level: debug/info/warn/error | No |

## Key Commands

### Go

```bash
buf generate                  # regenerate gRPC stubs from proto/
buf lint                      # lint proto files
go build ./...                # build all binaries
go test ./...                 # full test suite
go test ./internal/usecase/... # unit tests only
golangci-lint run             # lint
go run ./cmd/<project>ctl     # run CLI locally
```

### Python

```bash
uv sync                       # install dependencies
uv run pytest                 # unit tests (integration excluded by default)
uv run pytest -m integration  # integration tests only
uv run pytest -k "<name>"     # single test by name
uv run ruff check .           # lint
uv run ruff format .          # format
uv run mypy src/              # type check
```

## Observability — Prometheus Metrics (Mandatory)

Every gRPC method and REST endpoint **must** emit Prometheus metrics using the official SDK. No API or RPC ships without metrics.

### Go

Use `github.com/prometheus/client_golang/prometheus` and `promhttp`.

Required metrics per RPC method:

```go
// internal/infra/metrics/grpc.go
var (
    RPCDuration = prometheus.NewHistogramVec(
        prometheus.HistogramOpts{
            Name:    "<project>_grpc_duration_seconds",
            Buckets: prometheus.DefBuckets,
        },
        []string{"method", "status"},
    )
    RPCTotal = prometheus.NewCounterVec(
        prometheus.CounterOpts{Name: "<project>_grpc_requests_total"},
        []string{"method", "status"},
    )
)
```

Wire metrics into the gRPC server via `grpc.UnaryInterceptor` and expose the `/metrics` HTTP endpoint via `promhttp.Handler()` on a dedicated port (default `9090`). The REST gateway inherits coverage through the interceptor.

Labels on every metric: `method` (full gRPC method path), `status` (gRPC status code string).

### Python

Use the `prometheus-client` package. Instrument at the entrypoint layer using a middleware or decorator — never inside `usecase/` or `domain/`.

```python
# src/<project>/entrypoints/metrics.py
from prometheus_client import Counter, Histogram, start_http_server

REQUEST_DURATION = Histogram(
    "<project>_request_duration_seconds",
    "RPC/HTTP request duration",
    ["method", "status"],
)
REQUEST_TOTAL = Counter(
    "<project>_requests_total",
    "Total requests",
    ["method", "status"],
)
```

Call `start_http_server(9090)` at startup. FastAPI users: mount `make_asgi_app()` at `/metrics` instead of starting a separate server.

### Required Env Variables (add to existing table)

| Variable | Description | Required |
|---|---|---|
| `<PROJECT>_METRICS_PORT` | Prometheus scrape port (default 9090) | No |

---

## Feature Development Workflow

Every non-trivial feature follows this three-step planning sequence before any implementation begins:

### Step 1 — Brainstorm with Haiku

Use the `brainstorming` superpower with the `haiku` model to explore the feature space cheaply and fast.

```
/brainstorming --model haiku
```

Output: a rough plan capturing intent, scope boundaries, key decisions, and open questions. Save this as a plan file (`PLAN.md` or `docs/plans/<feature>.md`).

### Step 2 — Fine-tune with `/grill-me`

Run the `grill-me` skill (located at `skills/grill-me/SKILL.md` in this workspace) against the plan to surface blind spots, challenge assumptions, and sharpen scope.

```
/grill-me
```

This step refines the plan. Update the plan file with the outcome before proceeding.

### Step 3 — Generate PRD with `/to-prd`

Run the `to-prd` skill (at `../../gstack/to-prd/SKILL.md`) to convert the refined plan into a structured PRD artifact.

```
/to-prd
```

The PRD is written to `docs/prd/<feature>-prd.md`. Implementation does not start until the PRD exists.

> Note: `to-prd` is a custom skill targeted for this workspace. If the skill does not yet exist in `../../gstack/`, create it there before using this workflow.

### Enforcement

- No implementation task (proto changes, use case code, CLI command) may be started without a PRD in `docs/prd/`.
- Ralph loop prompts for this project must reference the PRD path as the source of truth for completion criteria.

---

## Dependencies & Versions

> Update this section when dependencies are pinned.

| Dependency | Version | Notes |
|---|---|---|
| `google.golang.org/grpc` | — | gRPC runtime |
| `github.com/grpc-ecosystem/grpc-gateway/v2` | — | REST gateway |
| `github.com/spf13/cobra` | — | CLI framework |
| `github.com/spf13/viper` | — | Config management |
| `buf` CLI | — | Proto toolchain |
| `github.com/prometheus/client_golang` | — | Go Prometheus SDK |
| Python | ≥3.12 | |
| `uv` | — | Package manager |
| `pytest` | — | Test runner |
| `ruff` | — | Lint + format |
| `mypy` | — | Type checking |
| `prometheus-client` | — | Python Prometheus SDK |

## Known Project-Specific Decisions

> Record any architectural decisions that deviate from `architecture.rules` here, with the reason.

_None yet._
