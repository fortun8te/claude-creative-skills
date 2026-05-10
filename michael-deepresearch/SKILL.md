---
name: michael:deepresearch
description: Use before strategy, positioning, or creative work. Combines fact-finding (what's true) with creative positioning (what others miss). Deploys parallel research agents, marks confidence levels, uncovers positioning gaps. Returns grounded insights + actionable angles. Fast, cost-efficient.
---

# Deep Research

Find what's true about a problem, then find what others missed.

One skill. Two parts: facts first, then positioning. Deploy parallel agents, get back grounded strategy.

## Checklist

1. **Understand the problem** — What are we researching? Why?
2. **Ask clarifying questions** — One at a time. Refine scope.
3. **Propose 2-3 research angles** — Different ways to approach it
4. **Deploy parallel agents** — Fact-finders + positioning scouts
5. **Review findings** — Facts + gaps + positioning
6. **Present insights** — Here's what's true. Here's what's missing.

## The Process

**Understanding the problem:**

- What are you actually trying to decide?
- Is it a market question? (What's growing? Why?)
- Is it a competitive question? (Why do they win? What do they miss?)
- Is it a positioning question? (What do we own that others don't?)

Don't overthink. One simple question framed one way.

**Clarifying questions (one at a time):**

- "Who would benefit from this research?"
- "What would change your strategy if you knew it?"
- "Horizontal or vertical? Existing market or new market?"

Ask until the problem is clear. Usually 1-2 questions.

**Propose 2-3 research angles:**

Angle A: **Deep facts** — Market size, growth rates, customer complaints, competitor positioning
Angle B: **Creative gaps** — What do winners own that losers don't? Cross-domain precedents.
Angle C: **Hybrid** — Facts on category, gaps on positioning. Which matters more for your decision?

Recommend the one that answers the decision.

**Deploy parallel agents:**

Create one task per angle:

```
Research angle: [Your angle]

Key questions:
- [Question 1]
- [Question 2]

Mark findings as:
- "Well-established" (≥2 sources, no major disagreement)
- "Contested" (sources disagree)
- "Low-confidence" (single source or emerging)

Return JSON:
{
  "findings": [{"claim": "...", "evidence": [...], "confidence": "..."}],
  "gaps": ["what remains unknown?"],
  "positioning_insight": "what do competitors miss?"
}
```

Each agent works independently. Takes 10-30 min depending on scope.

**Review findings:**

Read back:
- What's well-established? (Build strategy on this)
- What's contested? (Acknowledge the disagreement, pick your side)
- What's low-confidence? (Note it, flag for follow-up)
- What positioning gaps emerged? (This is the gold)

**Present insights:**

```
# Research: [Topic]

## Facts (Well-Established)
[List findings with sources]

## Contested
[What do smart people disagree on?]

## Positioning Gap (The Insight)
[What do competitors actually miss?]

## Next Steps
[What would we research if we had more time?]
```

That's it. Actionable, grounded, clear.

## Key Principles

- **One problem, not many** — If you're researching 5 unrelated things, split into 5 research tasks
- **Narrow scope** — "SaaS market" is too broad. "Why are vertical SaaS winning?" is right.
- **Confidence over certainty** — Mark what's solid. Acknowledge what's contested. Don't pretend you know things.
- **Positioning first, tactics second** — The research should answer "who do we serve and why?" Not "what features should we build?"

## Anti-Patterns

❌ "Research everything about the space" → Too broad, unfocused
✅ "Research why vertical SaaS is winning" → One clear question

❌ Treat contested findings as facts → Causes strategy whiplash
✅ Name the disagreement → "Market size is $50B (Gartner) or $200B (Coherent). Pick one."

❌ Research without deciding what matters → Analysis paralysis
✅ Frame research around a real decision → "Should we go vertical or horizontal?"

## Token Economy

- **Agents**: Use cheap models for fact-finding, stronger models for positioning gaps
- **Time cap**: 20-30 min per agent max (diminishing returns after)
- **Sources**: 3+ per major claim (stop researching once you have them)
- **Iterate once**: If findings conflict, run one follow-up. Not iterative refinement.

## Examples

See `references/example-research.md` for 3 worked examples:
- SaaS positioning (facts + gaps)
- Creator economy (market + positioning)
- B2B sales (cycle constraint as opportunity)

