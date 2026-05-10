# Graph Report - ai-skills  (2026-05-10)

## Corpus Check
- 21 files · ~18,470 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 595 nodes · 552 edges · 65 communities (43 shown, 22 thin omitted)
- Extraction: 98% EXTRACTED · 2% INFERRED · 0% AMBIGUOUS · INFERRED: 11 edges (avg confidence: 0.82)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `bfb92df1`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- [[_COMMUNITY_Project Config & Global Rules|Project Config & Global Rules]]
- [[_COMMUNITY_TDD Workflow & Git Checkpoints|TDD Workflow & Git Checkpoints]]
- [[_COMMUNITY_Feature Planning Pipeline|Feature Planning Pipeline]]
- [[_COMMUNITY_Interface Design & Dependency Injection|Interface Design & Dependency Injection]]
- [[_COMMUNITY_Red-Green-Refactor Cycle|Red-Green-Refactor Cycle]]
- [[_COMMUNITY_Deep Module Design|Deep Module Design]]
- [[_COMMUNITY_Mocking Strategies|Mocking Strategies]]
- [[_COMMUNITY_Behavior Over Implementation|Behavior Over Implementation]]
- [[_COMMUNITY_Clean Architecture (Go + Python)|Clean Architecture (Go + Python)]]
- [[_COMMUNITY_Testing Isolation & Integration|Testing Isolation & Integration]]
- [[_COMMUNITY_Table-Driven & Parametrize Tests|Table-Driven & Parametrize Tests]]
- [[_COMMUNITY_Vertical Slices & Issue Decomposition|Vertical Slices & Issue Decomposition]]
- [[_COMMUNITY_gRPC Gateway & Metrics|gRPC Gateway & Metrics]]
- [[_COMMUNITY_SDK-Style Interface Mocking|SDK-Style Interface Mocking]]
- [[_COMMUNITY_Functional Options Pattern|Functional Options Pattern]]
- [[_COMMUNITY_Go Error Wrapping|Go Error Wrapping]]
- [[_COMMUNITY_Context Propagation|Context Propagation]]
- [[_COMMUNITY_Fuzz Testing|Fuzz Testing]]
- [[_COMMUNITY_EAFP Python Idiom|EAFP Python Idiom]]
- [[_COMMUNITY_Pytest Fixtures|Pytest Fixtures]]
- [[_COMMUNITY_ADR Criteria|ADR Criteria]]
- [[_COMMUNITY_PRD Template|PRD Template]]
- [[_COMMUNITY_Jira MCP vs REST|Jira MCP vs REST]]
- [[_COMMUNITY_Guardrails Modes|Guardrails Modes]]
- [[_COMMUNITY_Parallel Agent Dispatch|Parallel Agent Dispatch]]
- [[_COMMUNITY_Scope Discipline|Scope Discipline]]
- [[_COMMUNITY_Community 26|Community 26]]
- [[_COMMUNITY_Community 27|Community 27]]
- [[_COMMUNITY_Community 28|Community 28]]
- [[_COMMUNITY_Community 29|Community 29]]
- [[_COMMUNITY_Community 30|Community 30]]
- [[_COMMUNITY_Community 31|Community 31]]
- [[_COMMUNITY_Community 32|Community 32]]
- [[_COMMUNITY_Community 33|Community 33]]
- [[_COMMUNITY_Community 34|Community 34]]
- [[_COMMUNITY_Community 35|Community 35]]
- [[_COMMUNITY_Community 36|Community 36]]
- [[_COMMUNITY_Community 37|Community 37]]
- [[_COMMUNITY_Community 38|Community 38]]
- [[_COMMUNITY_Community 39|Community 39]]
- [[_COMMUNITY_Community 40|Community 40]]
- [[_COMMUNITY_Community 41|Community 41]]
- [[_COMMUNITY_Community 42|Community 42]]
- [[_COMMUNITY_Community 43|Community 43]]
- [[_COMMUNITY_Community 44|Community 44]]
- [[_COMMUNITY_Community 45|Community 45]]
- [[_COMMUNITY_Community 46|Community 46]]
- [[_COMMUNITY_Community 47|Community 47]]
- [[_COMMUNITY_Community 48|Community 48]]
- [[_COMMUNITY_Community 49|Community 49]]
- [[_COMMUNITY_Community 50|Community 50]]
- [[_COMMUNITY_Community 51|Community 51]]
- [[_COMMUNITY_Community 52|Community 52]]
- [[_COMMUNITY_Community 53|Community 53]]
- [[_COMMUNITY_Community 54|Community 54]]
- [[_COMMUNITY_Community 55|Community 55]]
- [[_COMMUNITY_Community 56|Community 56]]
- [[_COMMUNITY_Community 57|Community 57]]
- [[_COMMUNITY_Community 58|Community 58]]
- [[_COMMUNITY_Community 59|Community 59]]
- [[_COMMUNITY_Community 60|Community 60]]
- [[_COMMUNITY_Community 61|Community 61]]
- [[_COMMUNITY_Community 62|Community 62]]
- [[_COMMUNITY_Community 63|Community 63]]
- [[_COMMUNITY_Community 64|Community 64]]

## God Nodes (most connected - your core abstractions)
1. `Python Testing Patterns` - 17 edges
2. `Go Testing Patterns` - 15 edges
3. `Python Development Patterns` - 15 edges
4. `Skills` - 12 edges
5. `Go Development Patterns` - 12 edges
6. `Test-Driven Development` - 11 edges
7. `Jira Integration Skill` - 10 edges
8. `TDD Workflow Skill` - 10 edges
9. `Project Configuration` - 9 edges
10. `tapas-engineering-toolkit` - 8 edges

## Surprising Connections (you probably didn't know these)
- `Global Development Guardrails (claude.md/global.md)` --semantically_similar_to--> `Guardrails Skill`  [INFERRED] [semantically similar]
  claude.md/global.md → skills/guardrails/SKILL.md
- `TDD Workflow Skill` --references--> `Refactor Candidates`  [EXTRACTED]
  skills/tdd/SKILL.md → plugins/tapas-engineering-toolkit/skills/tdd/refactoring.md
- `Accept Interfaces Return Structs Go Idiom` --semantically_similar_to--> `Dependency Injection for Testability`  [INFERRED] [semantically similar]
  skills/golang-patterns/SKILL.md → skills/tdd/interface-design.md
- `Protocol-Based Duck Typing` --semantically_similar_to--> `Accept Interfaces Return Structs Go Idiom`  [INFERRED] [semantically similar]
  skills/python-patterns/SKILL.md → skills/golang-patterns/SKILL.md
- `Clean Architecture Layers (domain → usecase → infra)` --semantically_similar_to--> `Python Clean Architecture (domain → usecase → infra → entrypoints)`  [INFERRED] [semantically similar]
  skills/golang-patterns/SKILL.md → skills/python-patterns/SKILL.md

## Hyperedges (group relationships)
- **Feature Development Planning Pipeline (Brainstorm → Grill-Me → To-PRD → To-Issues)** — readme_feature_development_workflow, skill_grillme_grill_me, skill_toprd_to_prd, skill_toissues_to_issues [EXTRACTED 1.00]
- **TDD Skill Reference Document Cluster** — skill_tdd_tdd_workflow, tdd_mocking_mocking_guidelines, tdd_tests_good_vs_bad_tests, tdd_deepmodules_deep_module_design, tdd_interfacedesign_interface_for_testability, tdd_refactoring_refactor_candidates [EXTRACTED 1.00]
- **Clean Architecture Pattern Shared Across Go and Python** — skill_golangpatterns_clean_architecture, skill_pythonpatterns_clean_architecture, claudemd_project_project_config [INFERRED 0.85]

## Communities (65 total, 22 thin omitted)

### Community 0 - "Project Config & Global Rules"
Cohesion: 0.04
Nodes (47): Anti-Patterns to Avoid, Avoid Package-Level State, Avoid String Concatenation in Loops, Avoiding Goroutine Leaks, code:go (func GracefulShutdown(server *http.Server) {), code:go (import "golang.org/x/sync/errgroup"), code:go (// Bad: Goroutine leak if context is cancelled), code:go (// Good: Single-method interfaces) (+39 more)

### Community 1 - "TDD Workflow & Git Checkpoints"
Cohesion: 0.04
Nodes (47): 1. Readability Counts, 2. Explicit is Better Than Implicit, 3. EAFP - Easier to Ask Forgiveness Than Permission, Anti-Patterns to Avoid, Basic Type Annotations, Class-Based Decorators, code:python (# Good: Clear and readable), code:python (# Good: Using context managers) (+39 more)

### Community 2 - "Feature Planning Pipeline"
Cohesion: 0.04
Nodes (47): Assertions, Async Fixture, Async Tests with pytest-asyncio, Basic Test Structure, Best Practices, code:python (# Step 1: Write failing test (RED)), code:python (# Mark slow tests), code:bash (# Run only fast tests) (+39 more)

### Community 3 - "Interface Design & Dependency Injection"
Cohesion: 0.06
Nodes (34): 1. Testable Requirements, 2. Test Types Needed, 3. Edge Cases & Error Scenarios, 4. Structured Analysis Output, Add a Comment, Analyzing a Ticket, Best Practices, code:json ({) (+26 more)

### Community 4 - "Red-Green-Refactor Cycle"
Cohesion: 0.07
Nodes (27): code:block1 (Project name:      <project>          # e.g. "auth", "order"), code:block2 (.), code:bash (buf generate                  # regenerate gRPC stubs from p), code:bash (uv sync                       # install dependencies), code:go (// internal/infra/metrics/grpc.go), code:python (# src/<project>/entrypoints/metrics.py), code:block7 (/brainstorming --model haiku), code:block8 (/grill-me) (+19 more)

### Community 5 - "Deep Module Design"
Cohesion: 0.08
Nodes (25): 1. Planning, 2. Tracer Bullet, 3. Incremental Loop, 4. Refactor, Anti-Pattern: Horizontal Slices, Checklist Per Cycle, CI/CD Integration, code:block1 (WRONG (horizontal):) (+17 more)

### Community 6 - "Mocking Strategies"
Cohesion: 0.08
Nodes (23): code:bash (# Add the marketplace), code:bash (claude plugin add /path/to/ai-skills/plugins/tapas-engineeri), code:block3 (1. /brainstorming --model haiku   → rough plan (cheap, fast)), code:block4 (tapas-engineering-toolkit/), Directory Structure, Feature Development Workflow, `golang-patterns`, `golang-testing` (+15 more)

### Community 7 - "Behavior Over Implementation"
Cohesion: 0.11
Nodes (17): code:block1 (agents/), code:block2 (agents/), code:block3 (Available agent domains:), code:block4 (Selected: Security Engineer + SEO Specialist), code:block5 (User: team builder), Configuration, Examples, How It Works (+9 more)

### Community 8 - "Clean Architecture (Go + Python)"
Cohesion: 0.12
Nodes (16): code:block1 (1. Read claude.md/architecture.rules (if present in the proj), code:block2 (Progress: [domain model ✓] [API contract ✓] [data layer — cu), code:markdown (# {Short title of the decision}), code:markdown (## Shared Understanding — [Feature Name]), Concrete scenarios, Fuzzy language, Glossary conflicts, /grill-me — Design Interview Skill (+8 more)

### Community 9 - "Testing Isolation & Integration"
Cohesion: 0.12
Nodes (15): Cancelling a Loop, code:block1 (/ralph-loop "<clear task description>" --completion-promise ), code:block2 (/ralph-loop "Implement the CreateOrder RPC: update proto, re), code:block3 (<promise>TASK COMPLETE</promise>), code:block4 (/cancel-ralph), Completion Signal, Global Development Guardrails, Guardrails (+7 more)

### Community 10 - "Table-Driven & Parametrize Tests"
Cohesion: 0.14
Nodes (15): Golang Testing Skill, Interface-Based Mocking in Go, Integration Test Isolation with Markers, Python Testing Skill, Git Checkpoint Commits at TDD Stages, Horizontal Slicing Anti-Pattern, RED-GREEN-REFACTOR Cycle, TDD Workflow Skill (+7 more)

### Community 11 - "Vertical Slices & Issue Decomposition"
Cohesion: 0.13
Nodes (15): Autouse Fixtures, Basic Fixture Usage, code:python (@pytest.fixture(autouse=True)), code:python (# tests/conftest.py), code:python (import pytest), code:python (@pytest.fixture), code:python (# Function scope (default) - runs for each test), code:python (@pytest.fixture(params=[1, 2, 3])) (+7 more)

### Community 12 - "gRPC Gateway & Metrics"
Cohesion: 0.13
Nodes (15): code:python (from unittest.mock import patch, Mock), code:python (@patch("mypackage.Database.connect")), code:python (@patch("mypackage.api_call")), code:python (@patch("builtins.open", new_callable=mock_open)), code:python (@patch("mypackage.DBConnection", autospec=True)), code:python (class TestUserService:), code:python (@pytest.fixture), Mock Class Instances (+7 more)

### Community 13 - "SDK-Style Interface Mocking"
Cohesion: 0.14
Nodes (13): code:block1 (Watched patterns:), code:block2 (/safety-guard freeze src/components/), code:block3 (/safety-guard guard --dir src/api/ --allow-read-all), code:block4 (/safety-guard off), guardrails — Prevent Destructive Operations, How It Works, Implementation, Integration (+5 more)

### Community 14 - "Functional Options Pattern"
Cohesion: 0.17
Nodes (11): A collection of steps I need to perform manually, code:bash (uvx graphify@0.14.0 --no-install), code:bash (uv tool install graphifyy && graphify install), code:block3 (/mcp-server run "uvx graphify@0.14.0 --no-install"), code:block4 (claude skill add safishamsi/graphify), code:block5 (/graphify .                        # build graph for current), code:block6 (# .graphifyignore), code:block7 (graphify-out/manifest.json    # mtime-based, breaks after gi) (+3 more)

### Community 15 - "Go Error Wrapping"
Cohesion: 0.17
Nodes (11): Best Practices, code:go (func TestHealthHandler(t *testing.T) {), code:bash (# Run all tests), code:yaml (# GitHub Actions example), code:go (var update = flag.Bool("update", false, "update golden files), Go Testing Patterns, Golden Files, HTTP Handler Testing (+3 more)

### Community 16 - "Context Propagation"
Cohesion: 0.17
Nodes (11): 1. Gather context, 2. Explore the codebase (optional), 3. Draft vertical slices, 4. Quiz the user, 5. Publish the issues to the issue tracker, Acceptance criteria, Blocked by, Parent (+3 more)

### Community 17 - "Fuzz Testing"
Cohesion: 0.2
Nodes (9): Adding New Plugins, Available Plugins, code:bash (# Add this marketplace to Claude Code), code:block2 (ai-skills/), License, Marketplace Structure, Plugin name rules, Quick Start (+1 more)

### Community 18 - "EAFP Python Idiom"
Cohesion: 0.22
Nodes (9): code:go (// Good: Wrap errors with context), code:go (// Define domain-specific errors), code:go (func HandleError(err error) {), code:go (// Bad: Ignoring error with blank identifier), Custom Error Types, Error Checking with errors.Is and errors.As, Error Handling Patterns, Error Wrapping with Context (+1 more)

### Community 19 - "Pytest Fixtures"
Cohesion: 0.22
Nodes (9): Basic Parametrization, code:python (@pytest.mark.parametrize("input,expected", [), code:python (@pytest.mark.parametrize("a,b,expected", [), code:python (@pytest.mark.parametrize("input,expected", [), code:python (@pytest.fixture(params=["sqlite", "postgresql", "mysql"])), Multiple Parameters, Parametrization, Parametrize with IDs (+1 more)

### Community 20 - "ADR Criteria"
Cohesion: 0.22
Nodes (8): Further Notes, Implementation Decisions, Out of Scope, Problem Statement, Process, Solution, Testing Decisions, User Stories

### Community 21 - "PRD Template"
Cohesion: 0.25
Nodes (8): Global Development Guardrails (claude.md/global.md), Project Configuration (claude.md/project.md), Decision Tree Interview Process, Grill-Me Design Interview Skill, Guardrails Skill, Jira Integration Skill, To-Issues Skill, To-PRD Skill

### Community 22 - "Jira MCP vs REST"
Cohesion: 0.29
Nodes (7): 1. Simplicity and Clarity, 2. Make the Zero Value Useful, 3. Accept Interfaces, Return Structs, code:go (// Good: Clear and direct), code:go (// Good: Zero value is useful), code:go (// Good: Accepts interface, returns concrete type), Core Principles

### Community 23 - "Guardrails Modes"
Cohesion: 0.29
Nodes (7): Basic Benchmarks, Benchmark with Different Sizes, Benchmarks, code:go (func BenchmarkProcess(b *testing.B) {), code:go (func BenchmarkSort(b *testing.B) {), code:go (func BenchmarkStringConcat(b *testing.B) {), Memory Allocation Benchmarks

### Community 24 - "Parallel Agent Dispatch"
Cohesion: 0.29
Nodes (7): code:python (class AppError(Exception):), code:python (# Good: Catch specific exceptions), code:python (def process_data(data: str) -> Result:), Custom Exception Hierarchy, Error Handling Patterns, Exception Chaining, Specific Exception Handling

### Community 25 - "Scope Discipline"
Cohesion: 0.29
Nodes (7): code:python (# Good: List comprehension for simple transformations), code:python (# Good: Generator for lazy evaluation), code:python (def read_large_file(path: str) -> Iterator[str]:), Comprehensions and Generators, Generator Expressions, Generator Functions, List Comprehensions

### Community 26 - "Community 26"
Cohesion: 0.29
Nodes (7): code:python (from dataclasses import dataclass, field), code:python (@dataclass), code:python (from typing import NamedTuple), Data Classes, Data Classes and Named Tuples, Data Classes with Validation, Named Tuples

### Community 27 - "Community 27"
Cohesion: 0.29
Nodes (7): Async/Await for Concurrent I/O, code:python (import concurrent.futures), code:python (def process_data(data: list[int]) -> int:), code:python (import asyncio), Concurrency Patterns, Multiprocessing for CPU-Bound Tasks, Threading for I/O-Bound Tasks

### Community 28 - "Community 28"
Cohesion: 0.29
Nodes (7): Avoid String Concatenation in Loops, code:python (# Bad: Regular class uses __dict__ (more memory)), code:python (# Bad: Returns full list in memory), code:python (# Bad: O(n²) due to string immutability), Generator for Large Data, Memory and Performance, Using __slots__ for Memory Efficiency

### Community 29 - "Community 29"
Cohesion: 0.29
Nodes (7): code:python (import tempfile), code:python (def test_with_tmp_path(tmp_path):), code:python (def test_with_tmpdir(tmpdir):), Testing File Operations, Testing Side Effects, Testing with pytest's tmp_path Fixture, Testing with tmpdir Fixture

### Community 30 - "Community 30"
Cohesion: 0.29
Nodes (7): code:python (@pytest.fixture), code:python (@pytest.fixture), code:python (class TestCalculator:), Common Patterns, Testing API Endpoints (FastAPI/Flask), Testing Class Methods, Testing Database Operations

### Community 31 - "Community 31"
Cohesion: 0.29
Nodes (6): Bad Tests, code:typescript (// GOOD: Tests observable behavior), code:typescript (// BAD: Tests implementation details), code:typescript (// BAD: Bypasses interface to verify), Good and Bad Tests, Good Tests

### Community 32 - "Community 32"
Cohesion: 0.33
Nodes (6): code:bash (# Basic coverage), code:go (//go:generate mockgen -source=interface.go -destination=mock), Coverage Targets, Excluding Generated Code from Coverage, Running Coverage, Test Coverage

### Community 33 - "Community 33"
Cohesion: 0.4
Nodes (5): code:go (func TestUser(t *testing.T) {), code:go (func TestParallel(t *testing.T) {), Organizing Related Tests, Parallel Subtests, Subtests and Sub-benchmarks

### Community 34 - "Community 34"
Cohesion: 0.4
Nodes (5): code:block1 (RED     → Write a failing test first), code:go (// Step 1: Define the interface/signature), Step-by-Step TDD in Go, TDD Workflow for Go, The RED-GREEN-REFACTOR Cycle

### Community 35 - "Community 35"
Cohesion: 0.4
Nodes (5): Basic Fuzz Test, code:go (func FuzzParseJSON(f *testing.F) {), code:go (func FuzzCompare(f *testing.F) {), Fuzz Test with Multiple Inputs, Fuzzing (Go 1.18+)

### Community 36 - "Community 36"
Cohesion: 0.4
Nodes (5): code:go (func setupTestDB(t *testing.T) *sql.DB {), code:go (func TestFileProcessing(t *testing.T) {), Helper Functions, Temporary Files and Directories, Test Helpers

### Community 37 - "Community 37"
Cohesion: 0.4
Nodes (4): code:typescript (// Easy to mock), code:typescript (// GOOD: Each function is independently mockable), Designing for Mockability, When to Mock

### Community 38 - "Community 38"
Cohesion: 0.5
Nodes (4): code:go (func TestAdd(t *testing.T) {), code:go (func TestParseConfig(t *testing.T) {), Table-Driven Tests, Table-Driven Tests with Error Cases

### Community 39 - "Community 39"
Cohesion: 0.5
Nodes (3): code:block1 (┌─────────────────────┐), code:block2 (┌─────────────────────────────────┐), Deep Modules

### Community 40 - "Community 40"
Cohesion: 0.5
Nodes (3): code:typescript (// Testable), code:typescript (// Testable), Interface Design for Testability

### Community 41 - "Community 41"
Cohesion: 0.5
Nodes (4): Accept Interfaces Return Structs Go Idiom, Protocol-Based Duck Typing, Dependency Injection for Testability, Mock at System Boundaries Only

### Community 42 - "Community 42"
Cohesion: 0.67
Nodes (3): code:go (// Define interface for dependencies), Interface-Based Mocking, Mocking with Interfaces

## Knowledge Gaps
- **312 isolated node(s):** `code:bash (# Add this marketplace to Claude Code)`, `Available Plugins`, `code:block2 (ai-skills/)`, `Plugin name rules`, `License` (+307 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **22 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Python Testing Patterns` connect `Feature Planning Pipeline` to `Vertical Slices & Issue Decomposition`, `gRPC Gateway & Metrics`, `Pytest Fixtures`, `Community 29`, `Community 30`?**
  _High betweenness centrality (0.026) - this node is a cross-community bridge._
- **Why does `Python Development Patterns` connect `TDD Workflow & Git Checkpoints` to `Parallel Agent Dispatch`, `Scope Discipline`, `Community 26`, `Community 27`, `Community 28`?**
  _High betweenness centrality (0.018) - this node is a cross-community bridge._
- **Why does `Go Development Patterns` connect `Project Config & Global Rules` to `EAFP Python Idiom`, `Jira MCP vs REST`?**
  _High betweenness centrality (0.010) - this node is a cross-community bridge._
- **What connects `code:bash (# Add this marketplace to Claude Code)`, `Available Plugins`, `code:block2 (ai-skills/)` to the rest of the system?**
  _312 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Project Config & Global Rules` be split into smaller, more focused modules?**
  _Cohesion score 0.04 - nodes in this community are weakly interconnected._
- **Should `TDD Workflow & Git Checkpoints` be split into smaller, more focused modules?**
  _Cohesion score 0.04 - nodes in this community are weakly interconnected._
- **Should `Feature Planning Pipeline` be split into smaller, more focused modules?**
  _Cohesion score 0.04 - nodes in this community are weakly interconnected._