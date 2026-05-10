---
name: execute-plan
description: Use to execute a strategy plan, feature spec, or creative brief into real deliverables (campaigns, code, content). Fresh subagent per task with staged review (spec-compliance + code-quality). Runtime smoke gates (dev server + browser + clean console + acceptance reproduced). Three-tier blocker escalation (self-research → debug subagent → ask user). Confidence-gated autonomy (green/yellow/red signals). Returns shipped work, not drafts.
---

# Execute Plan

Transform a strategy, specification, or brief into real, tested deliverables. Executes tasks via fresh subagents, verifies at runtime (not just in tests), and escalates blockers with escalating confidence signals.

## When to Use

- **After brainstorming**: You've validated an approach; now build it
- **Campaign execution**: Spec is locked; need ads/copy/social content
- **Product features**: Feature spec + design; build and ship
- **Creative briefs**: Brief is final; produce deliverables (video scripts, pitch decks, etc.)

Requires a spec or brief locked from previous phases. Don't use for exploration; use only for execution.

## Philosophy

**Fresh eyes per task.** Each task gets a new subagent. No context drift, no tunnel vision from previous work.

**Smoke gates beat unit tests.** Did you run the dev server? Does it work in the browser? Is the console clean? That matters more than a passing test.

**Confidence gates autonomy.** Red signals (unresolved blockers, hallucinated code) require user approval before continuing. Yellow signals get documented but proceed.

**Anti-hallucination discipline.** No TODOs, no stubs, no "as any", no unverified imports. Full code, always.

## The Process

### 1. Spec Review (Before Task Dispatch)

Read the spec/brief one more time. Check for:

- **Ambiguity**: Any requirement could be interpreted two ways? Resolve it.
- **Testability**: How will we know this is done? (Not "tests pass", but "user does X, gets Y")
- **Scope creep**: Does this pull in unrelated work? Cut it.
- **Dependencies**: Does this depend on something not yet delivered? Flag it.

Example testability frameworks:
- **Campaign**: "Run campaign for 1 week, achieve [X conversions] from [Y budget]"
- **Feature**: "User opens feature, does [action], result is [observable state]"
- **Content**: "Reader gets through content in X minutes, recalls 2 key points"

If spec fails any check, ask user to clarify before proceeding.

### 2. Decompose Into Independent Tasks

Break the work into tasks that:
- Can be executed independently (no blocking dependencies)
- Can be reviewed in isolation
- Produce tangible, testable output

Example decomposition:

**Campaign execution:**
- Task 1: Write headline + body copy variants (3 versions)
- Task 2: Design visual assets (hero image, CTA button, color palette)
- Task 3: Assemble campaign brief (targeting, budget, schedule)
- Task 4: Integration test (run mock campaign, verify all assets load, check for typos/brand consistency)

**Feature build:**
- Task 1: Implement core logic (algorithm, data flow, state management)
- Task 2: Build UI component (input form, output display)
- Task 3: Wire integration (component + logic connected end-to-end)
- Task 4: Polish (accessibility, responsive layout, error states)
- Task 5: Runtime smoke gate (dev server runs, no console errors, acceptance test passes)

No task should take >1 hour to review. If it does, split further.

### 3. Dispatch Each Task to Fresh Subagent

Create a focused task brief for each subagent:

```
TASK: [Task Name]

SPEC EXCERPT:
[Relevant part of spec/brief]

ACCEPTANCE CRITERIA:
- [Criterion 1: testable, observable]
- [Criterion 2: testable, observable]

FILES TO MODIFY/CREATE:
- [exact paths]

CONSTRAINTS:
- No TODOs, FIXMEs, stubs, or "as any" casts
- Verify all imports exist before including them
- Run [dev server / build / test] and confirm clean output
- If you hit a blocker you can't self-resolve in 10 min, escalate (see "Blocker Escalation")

SELF-REVIEW CHECKLIST:
- [ ] Code reads clean (no magic, names are clear)
- [ ] Acceptance criteria all met (testable proof required)
- [ ] Smoke gate passed (dev runs, console clean, acceptance reproduced)
- [ ] No hallucinated code (all imports verified, no fake APIs)

RETURN:
Commit message summary + links to changed files + smoke gate proof (screenshot or console output)
```

Each subagent works independently. Typical cycle: task dispatch → 20-30 min work → review → approve/request changes.

### 4. Staged Review (Two Passes)

Don't review all at once. Two passes:

**Pass 1: Spec Compliance**
- Does the output match the spec? (Is the campaign positioned correctly? Does the feature do what was asked?)
- Are acceptance criteria met? (Is there observable proof?)
- Any hallucinated code / broken imports? (Run tests or manual verification)

**Pass 2: Code/Creative Quality**
- Does the code/copy read clean? (Any confusing sections?)
- Does the design align with brand? (Colors, typography, tone)
- Any edge cases missed? (Error states, mobile layouts, edge inputs)

If Pass 1 fails, send back: "Doesn't meet spec. Fix X."
If Pass 2 fails, send back: "Meets spec, but fix quality issue Y."

### 5. Confidence Signals & Blocker Escalation

As you review, mark each task with a confidence signal:

**🟢 Green** — Spec-compliant, high quality, no blockers. Merge/ship immediately.

**🟡 Yellow** — Spec-compliant, but has a known limitation:
- Example: "Feature works, but mobile layout breaks on iPad" (acceptable for MVP)
- Document the limitation, ship with known gap
- Escalate to user only if the limitation changes requirements

**🔴 Red** — Blocker. Can't ship.
- Example: "Hallucinated API endpoint. Doesn't exist in codebase."
- Example: "Copy misrepresents product positioning."
- Example: "Feature breaks existing functionality."

For red signals: Stop. **Escalate immediately.**

### 6. Three-Tier Blocker Escalation

When a red signal hits:

**Tier 1: Self-Research (5 min)**
- Subagent re-reads spec, re-reviews code, identifies and fixes the blocker
- Example: "I hallucinated an API. Let me check the actual API and rewrite."
- If fixed: Ship with 🟢 Green
- If not fixed: → Tier 2

**Tier 2: Debug Subagent (10 min)**
- Fresh subagent reads the blocked task, spec, and feedback
- Task: "This code has a blocker. Fix it." (specific blocker stated)
- Subagent reworks the solution
- If fixed: Ship with 🟢 Green
- If not fixed: → Tier 3

**Tier 3: User Decision**
- Stop execution. Ask user:
  - "Task X blocked on [issue]. Here's what we tried. How should we proceed?"
  - Options: Clarify spec, scope cut, accept workaround, use different approach
  - User decides; execution resumes

Never try to work around a red signal. Escalate.

### 7. Runtime Smoke Gate

Before claiming "done", run the smoke gate:

**For code:**
1. Dev server starts cleanly (no build errors)
2. Open in browser; test acceptance criteria manually (not just automated tests)
3. Console is clean (no errors, warnings OK if intentional)
4. Acceptance criteria reproduced in browser (screenshot proof)

**For campaigns:**
1. All assets render (no broken images, fonts loaded)
2. Copy is free of typos (human read, not just spell-check)
3. Brand consistency check (colors match, tone is right, CTAs are aligned)
4. Run mock campaign (create sample email, social post, etc.; verify it looks right)

**For creative:**
1. Output matches brief (tone, length, format)
2. Human review (read, listen, or watch; it makes sense)
3. No typos or obvious errors
4. Accessibility check (alt text, contrast, captions if applicable)

Smoke gate is **not** "tests pass". It's "did you actually use it in a realistic way?"

If smoke gate fails, send back with specific findings. Don't accept "tests pass" as sufficient.

### 8. Re-Grounding Ritual

At the start of each task and after each blockers resolution:

1. **Re-read the spec** (30 seconds; remind yourself what "done" means)
2. **Check your assumptions** (Are you solving the right problem? Any new info since spec was locked?)
3. **Review the previous task's output** (Does this task build on the right foundation?)

Append to a shared `PROGRESS.md` file:

```markdown
## Task 2: Build UI Component

**Started**: [time]
**Spec re-read**: ✓ (feature must support dark mode; I missed this in initial design)
**Dependencies**: Task 1 output (state management) — verified available
**Assumption**: Users will interact via mouse (no touch). Spec says "mobile support" — REVISED to include touch

**Blockers encountered**: None
**Confidence**: 🟢 Green
**Ended**: [time]
```

This ritual prevents drift and creates a visible audit trail.

### 9. Anti-Hallucination Guards

Before accepting any task:

**Guard 1: Import verification**
- Every import in the code must exist in the codebase
- Subagent: "List all imports. Verify each exists via grep/search."
- If any import doesn't exist: Red signal → Tier 2 escalation

**Guard 2: No stubs**
- No `// TODO:`, `// FIXME:`, `throw new Error("not implemented")`, or `as any`
- Subagent: Grep the diff. Any of these? Red signal.

**Guard 3: API verification**
- Any external API call? Verify the endpoint exists + has correct payload shape
- Subagent: "Confirm this API endpoint exists and matches the payload."
- If hallucinated: Red signal → Tier 2

**Guard 4: Type safety**
- No `any` types unless absolutely justified (and documented)
- Builds and type-checks cleanly

Run guards before smoke gate. Fail fast.

## Checklist

- [ ] **Spec review** — Ambiguity resolved, testability defined, dependencies flagged
- [ ] **Decompose** — 4-7 independent tasks, each <1 hour to review
- [ ] **Task dispatch** — Each subagent has spec excerpt, acceptance criteria, constraints
- [ ] **Pass 1: Spec compliance** — Output matches spec, acceptance criteria met, no hallucinations
- [ ] **Pass 2: Quality** — Code/copy reads clean, brand-aligned, edge cases covered
- [ ] **Confidence signal** — 🟢 Green / 🟡 Yellow / 🔴 Red marked for each task
- [ ] **Blocker escalation** — Tier 1 (self) → Tier 2 (debug subagent) → Tier 3 (user decision)
- [ ] **Smoke gate** — Dev runs, browser test passes, console clean, acceptance reproduced
- [ ] **Anti-hallucination** — Imports verified, no stubs, APIs confirmed, types safe
- [ ] **PROGRESS.md** — Audit trail of assumptions, blockers, confidence signals

## Token Economy

- **Per-task subagent**: Fresh context, focused task (not inheriting prior context)
- **Review cost**: ~5K tokens per task (spec compliance + code quality + Guards)
- **Escalation cost**: Tier 2 debug = 1 fresh subagent; Tier 3 = user decision (stop burn)
- **Smoke gate**: Local work (no tokens); just verification

Hard caps:
- Max 2 Tier 2 escalations per task (if still blocked after 2, escalate to user)
- Max 3 revision rounds per task (if >3, pause and ask user to clarify spec)

## Anti-Patterns

❌ **Ship if tests pass** — Tests don't prove usability
✅ **Smoke gate** — Dev runs, browser works, acceptance reproduced

❌ **Review everything at once** — Overwhelm, miss issues
✅ **Two passes** — Spec compliance, then quality

❌ **Accept blockers as "known limitations"** — Rot
✅ **Escalate 🔴 red signals** — Force decision, don't work around

❌ **No anti-hallucination** — Ship broken code
✅ **Import verification, stub detection** — Catch before shipping

❌ **No audit trail** — Can't debug what went wrong
✅ **PROGRESS.md** — Record assumptions, blockers, confidence per task

## Examples

See `references/example-executions.md` for 3 worked examples:
- Campaign execution (4 tasks, 1 blocker, smoke gate proof)
- Feature build (5 tasks, 2 blockers, escalation to Tier 2)
- Creative brief (3 tasks, green across all, shipped in 1 cycle)

## Related Skills

- **brainstorming** — Use BEFORE this. You need validated approach first.
- **deep-research** — Referenced during spec review if assumptions need grounding.
- **creative-research** — Referenced if positioning needs validation.

