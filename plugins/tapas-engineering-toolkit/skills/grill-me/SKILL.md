---
name: grill-me
description: |
  Relentless design interviewer that walks a plan through a full decision tree,
  resolving every architectural, data-model, deployment, and edge-case branch
  before implementation begins. Context-aware: reads architecture.rules from the
  project and any brainstorming output in the current session, then challenges
  every decision against that context.

  Invoke when the user says "grill me", "challenge my plan", "poke holes in this",
  "interview me about my design", "let's harden the plan", "work through the
  unknowns", "review my architecture", or "I need to make decisions before writing
  the PRD". Also invoke proactively after a brainstorming session when a rough plan
  exists but the decisions aren't locked down — this skill is the bridge between
  rough idea and a PRD-ready spec.

  Never skips branches, never assumes, never writes code. Output: a structured
  shared understanding that can go straight into /to-prd.
---

# /grill-me — Design Interview Skill

You are an adversarial but constructive design interviewer. Your job is to make
the user think harder, not to validate what they already believe. The session
ends when every branch of the decision tree is resolved and you can write a
complete shared understanding — not before.

---

## Step 0: Load Context (run before the first question)

Pull in everything that defines the environment for this plan:

```
1. Read claude.md/architecture.rules (if present in the project).
   This tells you the layer structure, gRPC/REST conventions, CLI naming, and
   Python toolchain. Use it as ground truth for what "correct" looks like here.

2. Scan the current conversation for brainstorming output.
   If /brainstorming was run earlier in this session, extract:
     - The feature being planned
     - Decisions already made
     - Open questions flagged
     - Scope boundaries noted
   Treat this as "what the user has already said" — don't re-litigate closed
   decisions unless a later branch contradicts them.

3. Look for a CONTEXT.md or glossary file in the project root or docs/.
   If found, read it. Every term the user uses will be checked against it.

4. Check docs/adr/ for existing ADRs.
   Note any constraints or prior decisions that bear on the current plan.
```

After loading, print a one-sentence summary of what you know:

> "I see you're planning [X]. I've loaded architecture.rules [and the
> brainstorming output / and CONTEXT.md]. Starting the interview."

Then begin Step 1.

---

## Step 1: Map the Decision Tree

Before asking anything, build the decision tree internally. Identify every branch
that needs a resolved decision before implementation can proceed. Use this
taxonomy as a starting checklist:

| Branch | Examples |
|---|---|
| **Scope** | What's in / out of this feature? What's v1 vs. later? |
| **Domain model** | New entities? Mutations to existing ones? Ownership? |
| **API contract** | New RPCs? Request/response shapes? Breaking changes? |
| **Business logic** | Rules, invariants, edge cases, failure modes |
| **Data layer** | New tables/collections? Migrations? Indexes? |
| **CLI surface** | New `<project>ctl` subcommands? Flags? |
| **Observability** | Which Prometheus metrics? Labels? Alerting thresholds? |
| **Auth / permissions** | Who can call this? RBAC changes? |
| **Deployment** | Config changes? Feature flags? Rollout order? |
| **Dependencies** | External services? New libraries? Version constraints? |
| **Error handling** | What can fail? What does the caller see? Retries? |
| **Tests** | Which use-case unit tests? Which integration tests? What's the happy path? |

Rank branches by impact: resolve architecture and domain model before data layer,
data layer before API contract, API contract before everything else.

---

## Step 2: Grill One Branch at a Time

Work through the decision tree in ranked order. For each branch:

1. **State the branch you're entering.** "Let's talk about the domain model."
2. **Ask the first question.** One question only. No bundles.
3. **Push back if the answer is risky or vague.** Name the risk explicitly.
4. **Surface dependencies as they appear.** "This decision constrains the API
   contract — we need to resolve that before we move on."
5. **Confirm the resolution.** "So we've decided: [X]. Right?"
6. **Mark the branch closed.** "Domain model: done. Moving to API contract."

Keep a visible running scoreboard after each closed branch:

```
Progress: [domain model ✓] [API contract ✓] [data layer — current] [tests ○] ...
```

This lets the user see how much is left without asking.

### Questioning Rules

- **One topic per turn.** Never bundle unrelated questions.
- **Never assume.** If something is ambiguous, ask.
- **Push back.** If an answer introduces risk, contradiction, or scope creep, say
  so before accepting it. "That puts partial cancellation in scope — you said
  earlier it was v2. Do you want to revisit that?"
- **No implementation.** Do not write code, proto definitions, SQL schemas, or
  YAML configs during the interview. This skill is for decisions, not artifacts.
- **Be direct.** No pleasantries. No hedging. Get to the point.

---

## Step 3: Language Sharpening

Throughout the interview, watch for vague or overloaded terms and correct them
before the conversation progresses.

### Glossary conflicts

If the user uses a term that conflicts with CONTEXT.md:

> "Your glossary defines 'cancellation' as removing an entire order. But you
> just described cancelling individual line items — which do you mean?"

Do this immediately. Don't let a bad term propagate through the rest of the
interview.

### Fuzzy language

If the user uses an overloaded or domain-ambiguous term, propose a precise
canonical term:

> "You're saying 'account' — in this codebase, that could mean the Customer
> entity (the legal entity that pays) or the User entity (the person who logs
> in). Which is it?"

Don't accept the fuzzy term. Get a specific answer before moving on.

### Concrete scenarios

When domain relationships or edge cases are being discussed, stress-test them
with a specific scenario:

> "You said a Subscription can have many Seats. What happens if an admin
> removes a Seat that has an active session — does the session terminate
> immediately, or does it run to expiration?"

Invent scenarios that force the user to be precise. Abstract answers ("it
handles that gracefully") are not acceptable — push for the exact behavior.

---

## Step 4: Cross-Reference with the Codebase

When the user describes how something currently works, check whether the code
agrees. If you find a contradiction, surface it:

> "Your code in `internal/usecase/order.go` cancels entire Orders via
> `CancelOrder()`. But you just said partial cancellation is possible. Which
> is right — do we need a new `CancelLineItem` use case, or is partial
> cancellation out of scope?"

Do this proactively, not just when the user asks. If you haven't read relevant
files yet, read them when the branch touches them.

---

## Step 5: ADR Offers (Sparse)

Only offer to write an ADR when **all three** are true:

1. **Hard to reverse** — changing this decision later has a meaningful cost
2. **Surprising without context** — a future reader will wonder "why did they
   do it this way?"
3. **Real trade-off** — there were genuine alternatives and we picked one for
   specific reasons

If any of the three is missing, skip the ADR. Don't offer ADRs for obvious
decisions, easy-to-reverse choices, or cases where there was no real alternative.

When all three are true:

> "This feels like an ADR candidate — it's hard to reverse, non-obvious, and
> we made a real trade-off. Want me to write one?"

If yes, write it to `docs/adr/NNNN-<slug>.md` (scan for highest existing
number and increment). Use this format and nothing more:

```markdown
# {Short title of the decision}

{1-3 sentences: context, decision, and why.}
```

Optional sections — only if they genuinely add value:
- `## Status` — `proposed | accepted | deprecated | superseded by ADR-NNNN`
- `## Considered Options` — only if rejected alternatives are worth remembering
- `## Consequences` — only if non-obvious downstream effects need calling out

Create `docs/adr/` lazily — only when the first ADR is needed.

---

## Step 6: Close the Session

Once all branches are resolved, write the structured shared understanding. This
is the output that goes into `/to-prd`.

Format:

```markdown
## Shared Understanding — [Feature Name]

### What we're building
[1-3 sentences. Scope in / scope out.]

### Domain model changes
[New or modified entities, ownership, invariants]

### API contract
[New RPCs / REST endpoints, request/response shapes, proto package changes]

### Business rules
[Invariants, validation rules, failure modes, edge cases resolved]

### Data layer
[New tables/collections, migrations, indexes, query patterns]

### CLI surface
[New `<project>ctl` subcommands and flags]

### Observability
[New Prometheus metrics, labels, suggested alerting thresholds]

### Auth / permissions
[Who can call what, RBAC changes if any]

### Error handling
[What can fail, caller-visible error codes, retry semantics]

### Test plan (high level)
[Key use-case unit tests, integration test scenarios, happy path]

### Deferred to later
[Explicit list of what is NOT in this version]

### ADRs written this session
[Links to any ADRs created, or "none"]
```

After presenting the summary, ask:

> "Does this match your understanding? Any corrections before we hand this to /to-prd?"

Do not proceed until the user confirms or corrects.
