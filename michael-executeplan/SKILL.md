---
name: michael:executeplan
description: Use to ship strategy into reality. Takes a locked spec/brief and executes it. Per-task subagents with staged review. Runtime smoke gates (dev + browser + clean console). Blockers escalate 3-tier. Returns shipped work, not drafts.
---

# Execute Plan

Ship it.

You have a strategy or spec locked. Now execute it. Each task gets a fresh subagent. Each task gets reviewed twice: spec compliance, then quality.

## Checklist

1. **Lock the spec** — No ambiguity. Here's done.
2. **Break into tasks** — Independent, testable, reviewable
3. **Dispatch per-task subagents** — Fresh eyes per task
4. **Review: Spec compliance** — Does it match the spec?
5. **Review: Quality** — Does it read clean? Edge cases covered?
6. **Smoke gate** — Dev runs? Browser works? Console clean?
7. **Ship** — Merge and move on

## The Process

**Lock the spec:**

Does the brief have ambiguity? Fix it.
- "Write copy" vs. "Write 3 headline variants" (be specific)
- "Build feature" vs. "Build feature with acceptance criteria" (define done)

If you can't answer "how will I know this is done?", the spec isn't locked.

**Break into tasks:**

4-7 tasks typically. Each:
- Can be done independently
- Has clear acceptance criteria (testable)
- Produces one deliverable

Example decomposition:
- Task 1: Copy variants (3 versions)
- Task 2: Visual design (hero image)
- Task 3: Integration (wire copy + design)
- Task 4: Polish (accessibility, mobile)
- Task 5: Smoke gate (verify it works end-to-end)

**Dispatch subagents:**

For each task:

```
TASK: [Task name]

SPEC EXCERPT:
[Relevant spec section]

ACCEPTANCE CRITERIA:
- [Criterion 1: testable]
- [Criterion 2: testable]
- [Criterion 3: testable]

CONSTRAINTS:
- No TODOs, FIXMEs, stubs
- Verify all imports/APIs exist
- Run [dev / build / test]. Output must be clean.

RETURN:
Summary + proof (screenshot or output log)
```

Each subagent works independently. 20-30 min typical.

**Review: Spec compliance:**

Does the output match the spec? 
- Are acceptance criteria met?
- Any hallucinated code/APIs?
- Any missing pieces?

If no: Send back. "Doesn't meet spec. Fix X."

**Review: Quality:**

Does it read clean?
- Code: Any confusing sections?
- Copy: Typos? Brand voice aligned?
- Design: Mobile-responsive? Accessible?

If no: Send back. "Meets spec, but fix quality issue Y."

**Smoke gate:**

Before shipping:
- Dev server starts cleanly (no errors)
- Open in browser; run acceptance test manually (not just automated)
- Console is clean (errors OK if documented)
- One person: "Does this actually work?"

If no: Send back. "Smoke gate failed on X."

**Ship:**

Merge, push, done.

## Confidence Signals

For each task:

**🟢 Green** — Spec-compliant, high quality, no blockers. Ship.

**🟡 Yellow** — Spec-compliant, but has a known limitation. Ship with note.

**🔴 Red** — Blocker. Can't ship.
- Example: "Hallucinated API endpoint"
- Example: "Copy misrepresents positioning"

For red: Stop. Escalate.

## Blocker Escalation

Tier 1 (5 min): Subagent re-reads spec, identifies fix themselves.
Tier 2 (10 min): Fresh subagent tackles the blocker.
Tier 3: Ask user. "Can't resolve. Here are options."

## Key Principles

- **Spec first** — Locked spec, not fuzzy guidelines
- **Independent tasks** — One subagent per task
- **Two-pass review** — Spec, then quality
- **Smoke gates, not tests** — Does it work in reality?
- **No hallucinations** — Verify imports, no stubs, clean code

## Anti-Patterns

❌ Ship if tests pass → Tests don't prove usability
✅ Smoke gate → Dev runs, browser works, console clean

❌ Review everything at once → Overwhelm, miss issues
✅ Two passes → Spec compliance, then quality

❌ Accept hallucinated code → Breaks in production
✅ Verify imports → Every API must exist

❌ Fuzzy done → "Looks pretty good?"
✅ Testable criteria → Acceptance test passes

## Examples

See `references/example-executions.md` for worked examples.

