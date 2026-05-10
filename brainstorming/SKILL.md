---
name: brainstorming
description: Use when you need to generate ideas, strategies, or solutions for a creative brief. Requires deep-research and creative-research findings first. Recon pass before questions. Generates 2-3 worldview-axis approaches with real tradeoffs. Runs adversarial pre-pass (reframe + premortem + red-team) at three checkpoints. Bundled multi-choice questions reveal tensions. Returns frameworks + actionable ideas, not lists.
---

# Brainstorming

Generate strategies, ideas, or solutions for creative briefs. Requires research anchoring first (deep-research + creative-research). Runs a recon pass, generates worldview-axis approaches, and includes adversarial pre-passes at key checkpoints to avoid false consensus.

## When to Use

- **After research**: You've done deep-research (market data) + creative-research (positioning gaps) and now need ideas
- **Strategic decisions**: "Given what we know, should we build/buy/partner?" "Sync or async? Local or cloud?"
- **Creative briefs**: "How do we position this product?" "What's the campaign angle?"
- **Product direction**: "Where should we double down?" "What's the one thing we should own?"

Use this ONLY after deep-research + creative-research. Brainstorming without research anchoring is speculation.

## Philosophy

**Ideas without constraints are noise.** Constraints (from research) make ideas valuable.

**Approaches beat lists.** Return 2-3 coherent strategies with real tradeoffs, not 10 unordered ideas.

**Adversarial thinking prevents groupthink.** Reframe, premortem, red-team at key checkpoints before finalizing.

**Worldview axes** beat feature brainstorms. How do you THINK about the problem? That determines which ideas matter.

## The Process

### Phase 1: Recon (No Ideation Yet)

Read your research findings (deep + creative). Don't ideate yet. Instead:

1. **Map the research landscape**:
   - What's well-established? (facts you can build on)
   - What's contested? (tensions/disagreements to navigate)
   - What's a gap? (unknowns worth deciding on)

2. **Identify the real decision**:
   - "Should we target segment A or B?" (positioning choice)
   - "Should we own speed or depth?" (value choice)
   - "Build in-house or partner?" (execution choice)

3. **List constraints & tensions**:
   - Resource constraints (budget, team, time)
   - Market constraints (adoption barriers, willingness to pay)
   - Creative tensions (what can't we do if we own X?)

**Don't move forward until you're clear on the real decision.** Most brainstorming fails because people are solving different problems.

### Phase 2: Worldview-Axis Approaches

Instead of "brainstorm ideas", generate 2-3 **approaches** using worldview axes:

**Axis 1**: HOW DO WE THINK ABOUT TIME?
- Option A: "Quick wins build momentum" (emphasize speed, iterate fast, gather feedback early)
- Option B: "Deep foundation prevents tech debt" (emphasize stability, research before building, slow is smooth)

**Axis 2**: HOW DO WE THINK ABOUT USERS?
- Option A: "Segment the market vertically" (serve one industry deeply)
- Option B: "Serve horizontally across use cases" (broad appeal, multi-use-case)

**Axis 3**: HOW DO WE THINK ABOUT RISK?
- Option A: "Experimentation is learning" (embrace small failures, iterate)
- Option B: "Prevention beats cure" (reduce risk upfront, plan carefully)

For each **axis**, generate 1-2 ideas that flow from that worldview:

```
AXIS: Quick wins vs. deep foundation

Under "Quick Wins":
- Idea 1: Rapid prototyping with low-fi mockups, user feedback in week 1
- Idea 2: MVP with 3 core features + community feedback loop
- Trade-off: May discover architectural limits later; may need refactor

Under "Deep Foundation":
- Idea 1: 6-week research sprint before any design/code
- Idea 2: Spec-first approach; code only after design is locked
- Trade-off: Slower launch; higher confidence in direction
```

Aim for **2-3 axes**, each generating 1-2 ideas. That's 4-6 ideas arranged by worldview, not a list.

### Phase 3: Bundled Multi-Choice Questions

Present worldview axes as BUNDLED questions (not one-by-one):

**Question 1: Time & Iteration**
- A) Quick wins + iterate (ship fast, gather feedback)
- B) Deep foundation + lock direction (plan before build)
- C) Hybrid (4-week sprint, then iterate)

*Why these options?* Real-world precedents:
- A: Figma, Canva (fast iteration drove adoption)
- B: Apple (lock direction, then scale)
- C: Amazon (6-pager + working backward, then iterate)

**Question 2: Segment vs. Horizontal**
- A) Serve one vertical deeply (e.g., "only for architects")
- B) Horizontal appeal across use cases (e.g., "any professional")
- C) Start vertical, expand horizontally over time

*Why these options?*
- A: Slack (started with teams, now all-purpose)
- B: Notion (tried to be all-purpose from day 1)
- C: Figma (design teams → all designers → product managers)

Frame multi-choice questions to **reveal tensions**, not hide them. The user picks which tension they can live with.

### Phase 4: Adversarial Pre-Pass (Three Checkpoints)

At three points, run adversarial passes:

**Checkpoint 1: Reframe (after initial ideas)**
- "What if we're solving the wrong problem?" 
- "What if the market doesn't care about what we think matters?"
- "Reframe your strongest idea in 1-2 sentences. Now argue against it."

**Checkpoint 2: Premortem (before committing to approach)**
- "It's 18 months from now. We chose approach X and it failed. What killed it?"
- "What would we have needed to know in advance to avoid this failure?"
- "What's the one assumption that, if wrong, makes this entire approach invalid?"

**Checkpoint 3: Red Team (final synthesis)**
- "How would a competitor exploit this idea's weaknesses?"
- "What market shift would make this idea irrelevant in 12 months?"
- "If we're right about positioning, what WOULDN'T we do? (What would we deliberately avoid?)"

Document the adversarial findings alongside your recommendations. They're not negatives; they're risk mitigation.

## Checklist

- [ ] **Recon pass** — Read research, identify the real decision, list constraints
- [ ] **Worldview axes** — Generate 2-3 axes (time, users, risk, etc.) + 1-2 ideas per axis
- [ ] **Multi-choice questions** — Frame worldview choices as bundled, real-world-informed options
- [ ] **Checkpoint 1: Reframe** — Argue against strongest idea; identify hidden assumptions
- [ ] **Checkpoint 2: Premortem** — What would kill this idea? What's the critical assumption?
- [ ] **Checkpoint 3: Red Team** — How would competitor exploit this? What market shifts kill it?
- [ ] **Synthesis** — Present 2-3 approaches + adversarial findings + recommended path forward

## Format: Approaches, Not Lists

❌ **Bad format** (lists):
```
Ideas:
1. Launch with influencer partnerships
2. Build a community
3. Run early access
4. Create educational content
5. Partner with platforms
...
```

✅ **Good format** (approaches):
```
## Approach A: Community-First
- Idea: Launch in tight community (early architects on Twitter), gather feedback, expand
- Worldview: User advocacy matters more than scale initially
- Trade-off: Slower launch but highly defensible positioning
- Risk: Stays niche if community doesn't expand

## Approach B: Platform Partnership
- Idea: Launch embedded in existing tool (Adobe plugin), reach 10K users via platform
- Worldview: Distribution beats word-of-mouth for adoption
- Trade-off: Less positioning control; dependent on partner
- Risk: Partner changes strategy, kills integration

## Approach C: Hybrid
- Idea: 3-month community phase, then platform partnership
- Worldview: Build credibility first, then scale via distribution
- Trade-off: Slower overall, requires two launches
- Risk: Community momentum lost during partner negotiations
```

Each approach is a coherent strategy, not a tactic. Users pick which tradeoff they can live with.

## Token Economy

- **Recon**: Use model locally (no tokens); read research, map landscape
- **Ideation**: Use strong model (Qwen 3.5 4b–9b) for worldview axes + approaches
- **Adversarial**: Use strong model for reframe/premortem/red-team (worth the tokens; prevents costly pivots)

Hard caps:
- Max 3 worldview axes per brainstorm (beyond this is analysis fatigue)
- 1-2 ideas per axis (focused, not exhaustive)
- 1 adversarial pass per checkpoint (3 total, not iterative)

## Anti-Patterns

❌ **Lists of ideas** — "10 campaign concepts!" (Unfocused, no tradeoffs)
✅ **2-3 coherent approaches** — "Here are 3 strategies; pick which tradeoff fits"

❌ **No research grounding** — "Let's brainstorm!" (Speculation)
✅ **Anchored in research** — "Given the market gaps we found, here are approaches"

❌ **Single worldview** — All ideas optimize for speed (or cost, or scale)
✅ **Multiple worldviews** — Trade-off between speed/depth, vertical/horizontal, risk/reward

❌ **No adversarial thinking** — Present ideas as winning
✅ **Adversarial pre-pass** — "Here's how this could fail; here's what we'd need to know"

## Examples

See `references/example-brainstorms.md` for 3 worked examples:
- SaaS positioning (market data → worldview axes → community-first vs. platform-first vs. hybrid)
- Creator tool strategy (research gaps → reframe/premortem → 3 approaches)
- B2B campaign direction (research + positioning → adversarial thinking → recommended path)

## Related Skills

- **deep-research** — Use BEFORE this. Ground brainstorming in facts.
- **creative-research** — Use BEFORE this. Inform worldview axes with positioning gaps.
- **execute-plan** — Use AFTER this. Test approaches in real campaigns/products.

