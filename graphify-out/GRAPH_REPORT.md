# Graph Report - .  (2026-05-10)

## Corpus Check
- Corpus is ~17,983 words - fits in a single context window. You may not need a graph.

## Summary
- 57 nodes · 50 edges · 26 communities (6 shown, 20 thin omitted)
- Extraction: 74% EXTRACTED · 26% INFERRED · 0% AMBIGUOUS · INFERRED: 13 edges (avg confidence: 0.84)
- Token cost: 78,974 input · 0 output

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

## God Nodes (most connected - your core abstractions)
1. `tapas-claude-toolkit Plugin` - 13 edges
2. `TDD Workflow Skill` - 13 edges
3. `Grill-Me Design Interview Skill` - 4 edges
4. `To-PRD Skill` - 4 edges
5. `Project Configuration (claude.md/project.md)` - 4 edges
6. `Feature Development Workflow (Brainstorm → Grill → PRD)` - 3 edges
7. `Deep Module Design Principle` - 3 edges
8. `Golang Testing Skill` - 3 edges
9. `To-Issues Skill` - 3 edges
10. `Global Development Guardrails (claude.md/global.md)` - 3 edges

## Surprising Connections (you probably didn't know these)
- `Global Development Guardrails (claude.md/global.md)` --semantically_similar_to--> `Guardrails Skill`  [INFERRED] [semantically similar]
  claude.md/global.md → skills/guardrails/SKILL.md
- `tapas-claude-toolkit Plugin` --references--> `Python Testing Skill`  [EXTRACTED]
  README.md → skills/python-testing/SKILL.md
- `TDD Workflow Skill` --conceptually_related_to--> `Vertical Slices Over Horizontal Layers Principle`  [EXTRACTED]
  skills/tdd/SKILL.md → README.md
- `TDD Workflow Skill` --conceptually_related_to--> `Behavior Over Implementation Testing Principle`  [EXTRACTED]
  skills/tdd/SKILL.md → README.md
- `tapas-claude-toolkit Plugin` --references--> `TDD Workflow Skill`  [EXTRACTED]
  README.md → skills/tdd/SKILL.md

## Hyperedges (group relationships)
- **Feature Development Planning Pipeline (Brainstorm → Grill-Me → To-PRD → To-Issues)** — readme_feature_development_workflow, skill_grillme_grill_me, skill_toprd_to_prd, skill_toissues_to_issues [EXTRACTED 1.00]
- **TDD Skill Reference Document Cluster** — skill_tdd_tdd_workflow, tdd_mocking_mocking_guidelines, tdd_tests_good_vs_bad_tests, tdd_deepmodules_deep_module_design, tdd_interfacedesign_interface_for_testability, tdd_refactoring_refactor_candidates [EXTRACTED 1.00]
- **Clean Architecture Pattern Shared Across Go and Python** — skill_golangpatterns_clean_architecture, skill_pythonpatterns_clean_architecture, claudemd_project_project_config [INFERRED 0.85]

## Communities (26 total, 20 thin omitted)

### Community 0 - "Project Config & Global Rules"
Cohesion: 0.27
Nodes (10): Global Development Guardrails (claude.md/global.md), Project Configuration (claude.md/project.md), tapas-claude-toolkit Plugin, Golang Patterns Skill, Decision Tree Interview Process, Guardrails Skill, Jira Integration Skill, Python Patterns Skill (+2 more)

### Community 1 - "TDD Workflow & Git Checkpoints"
Cohesion: 0.4
Nodes (5): Python Testing Skill, Git Checkpoint Commits at TDD Stages, TDD Workflow Skill, Refactoring Candidates After TDD Cycle, Good vs Bad Tests Reference

### Community 2 - "Feature Planning Pipeline"
Cohesion: 0.5
Nodes (5): Ralph Loop Workflow, Ralph Loop Iterative Development Workflow, Feature Development Workflow (Brainstorm → Grill → PRD), Grill-Me Design Interview Skill, To-PRD Skill

### Community 3 - "Interface Design & Dependency Injection"
Cohesion: 0.5
Nodes (4): Accept Interfaces Return Structs Go Idiom, Protocol-Based Duck Typing, Dependency Injection for Testability, Mock at System Boundaries Only

### Community 4 - "Red-Green-Refactor Cycle"
Cohesion: 0.67
Nodes (3): Horizontal Slicing Anti-Pattern, RED-GREEN-REFACTOR Cycle, Tracer Bullet TDD Pattern

### Community 5 - "Deep Module Design"
Cohesion: 0.67
Nodes (3): Deep Module Extraction During PRD, Deep Module Design Principle, Interface Design for Testability

## Knowledge Gaps
- **34 isolated node(s):** `Git Checkpoint Commits at TDD Stages`, `Mock at System Boundaries Only`, `SDK-Style Interfaces for Mockability`, `Good vs Bad Tests Reference`, `Behavior-Based Testing (Test Through Public Interfaces)` (+29 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **20 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `TDD Workflow Skill` connect `TDD Workflow & Git Checkpoints` to `Project Config & Global Rules`, `Red-Green-Refactor Cycle`, `Deep Module Design`, `Mocking Strategies`, `Behavior Over Implementation`, `Testing Isolation & Integration`, `Vertical Slices & Issue Decomposition`?**
  _High betweenness centrality (0.239) - this node is a cross-community bridge._
- **Why does `tapas-claude-toolkit Plugin` connect `Project Config & Global Rules` to `TDD Workflow & Git Checkpoints`, `Feature Planning Pipeline`, `Testing Isolation & Integration`?**
  _High betweenness centrality (0.211) - this node is a cross-community bridge._
- **What connects `Git Checkpoint Commits at TDD Stages`, `Mock at System Boundaries Only`, `SDK-Style Interfaces for Mockability` to the rest of the system?**
  _34 weakly-connected nodes found - possible documentation gaps or missing edges._