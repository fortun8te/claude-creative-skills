---
name: deep-research
description: Use when you need to research a topic deeply for strategy, positioning, market gaps, or expert-level understanding. Dispatches parallel research subagents with adversarial verification, confidence bands, and depth-2 decomposition. Returns high-confidence findings with documented sources and key gaps. Fast, cost-efficient (cheap workers, strong synthesis), real-world ready.
---

# Deep Research

Research complex topics for strategy, competitive positioning, market analysis, or expert-level understanding. Dispatches parallel subagents with orchestration, searches claim negations, marks findings with confidence bands instead of numeric scores, and documents gaps.

## When to Use

- **Strategy questions**: "What's the real positioning gap in productivity software?"
- **Market analysis**: "What's driving adoption of vertical SaaS in [domain]?"
- **Competitive research**: "Why is competitor X winning in segment Y?"
- **Expert gaps**: "What do top practitioners disagree on in [field]?"
- **Constraint discovery**: "What are the hard limits in [technology/market]?"

Use this BEFORE brainstorming or creative-research. It anchors all downstream thinking.

## The Process

### 1. Recon Pass (No Search Yet)

Before dispatching subagents, ground yourself:
- Skim existing knowledge gaps (what do you NOT know?)
- Estimate research scope (narrow/broad/very broad?)
- Identify domain (tech, business, culture, science, design?)
- List your assumptions (what are you taking as fact?)

This takes 2-3 minutes and prevents unfocused sprawl.

### 2. Decompose Into Depth-2 Subquestions

Don't research "productivity software market". Instead:

**Level 1 (what):**
- Market size and growth rate
- Key use cases driving adoption
- Positioning gaps vs. incumbents

**Level 2 (why):**
- *Under "market size"*: What's changed in the last 18mo? Why?
- *Under "key use cases"*: Which segment is fastest-growing? Why that segment?
- *Under "positioning gaps"*: What do users complain about in top 3 players?

For each Level 1 question, identify 1-2 Level 2 dives. Don't go deeper than Level 2 unless scope justifies it (rare). Append your gap justification to the research task.

### 3. Dispatch Parallel Subagents

Create a research task for each Level 1 question (3-5 subagents typically):

```
Task: Research [specific subquestion]

Focus areas:
- [Level 2 dive 1]
- [Level 2 dive 2]

Sources to prioritize:
- Market reports (Gartner, Mordor, Coherent, etc.)
- Reddit threads / forums (real user complaints)
- Job postings (infer what skills/problems are hot)
- Investor decks / Twitter from founders
- Academic research (if domain-specific)

Confidence marking:
- Mark EACH finding as one of:
  - "well-established" (≥2 independent sources, contradictions <5%)
  - "contested" (sources disagree, or <2 sources on emerging fact)
  - "low-confidence" (single source or speculation)

Return a JSON block with:
{
  "question": "...",
  "findings": [
    {"claim": "...", "evidence": [...], "confidence": "well-established"}
  ],
  "gaps": ["what questions remain?"],
  "sources": ["url1", "url2", ...]
}
```

Each subagent works in parallel. Typical runtime: 10-30 min per agent depending on scope.

### 4. Adversarial Verification (Optional, High-Value)

For any claim marked "well-established", spawn ONE verification subagent:

```
Task: Find evidence AGAINST this claim: "[claim]"

Search for:
- Direct refutations
- Contradictory data
- Exception cases / edge cases
- Expert disagreement

If you find ≥1 independent source contradicting the claim, escalate to "contested".
If you find nothing contradicting it after 5 min of searching, mark it "well-established".

Return:
{
  "claim": "...",
  "counter_evidence": [...],
  "final_confidence": "well-established" | "contested" | "low-confidence"
}
```

This flips the search bias (avoid confirmation bias) and costs only 1 extra agent.

### 5. Synthesis

Aggregate findings into a research report:

```markdown
# Research Report: [Topic]

## Key Findings (Well-Established)

[List all "well-established" claims with 1-2 supporting quotes/sources]

## Contested/Emerging Findings

[List all "contested" claims; show both sides of disagreement]

## Low-Confidence Observations

[List single-source findings marked for follow-up]

## Positioning Gaps (Strategic Insight)

[Your synthesis: what do competitors NOT own? What do users complain about universally?]

## Research Gaps & Next Steps

[What would change the strategy if we knew it? What's worth a 2nd research pass?]

## Sources

[Ranked by reliability: market reports, expert interviews, user data, speculation]
```

## Checklist

- [ ] **Recon Pass** — Identify knowledge gaps, estimate scope, list assumptions
- [ ] **Decompose** — Level 1 questions + Level 2 dives + gap justifications
- [ ] **Dispatch Subagents** — 3-5 parallel agents, each with a clear subquestion
- [ ] **Wait for Completion** — Typical 10-30 min per agent (depends on scope)
- [ ] **Adversarial Verification** (optional) — Spawn 1 agent per "well-established" claim to find contradictions
- [ ] **Synthesis** — Aggregate into report with gap analysis + strategic insights
- [ ] **Document Sources** — All URLs, models used, search queries in audit trail

## Token Economy

- **Workers**: Use cheap models (Qwen 3.5 0.8b–2b) for web research + compression
- **Synthesis**: Use strong model (Qwen 3.5 4b–9b) only for final aggregation + gap analysis
- **Hard caps**: 
  - Max 5 subagents per research (avoid analysis paralysis)
  - Max 20 min per subagent (diminishing returns after 30 min)
  - Max 10 searches per subagent (stop once you have ≥2 sources per claim)
- **Reuse**: Cache research findings in IndexedDB or shared context for downstream tasks (brainstorming, creative-research)

## Anti-Patterns

❌ **Too broad** — "Research AI industry" → 100 subagents, no focus
✅ **Right scope** — "Research LLM fine-tuning cost trends" → 3-5 focused subagents

❌ **Too many levels** — Decompose to Level 3, 4, 5 → diminishing returns
✅ **Right depth** — Level 1 + 1-2 Level 2 dives per question

❌ **No confidence marking** — "The market is $50B" (says who?)
✅ **Explicit confidence** — "Market size is $50B (well-established: Gartner 2024 + Coherent Markets)" 

❌ **Single source as truth** — One Reddit thread = universal user complaint
✅ **Cross-validation** — If only one source found, mark "low-confidence" and flag for follow-up

## Examples

See `references/example-research-reports.md` for 3 worked examples:
- SaaS market positioning (3 subagents, 2 verification passes)
- Vertical AI adoption drivers (4 subagents, 1 verification)
- Design system tooling gaps (5 subagents, adversarial pass on "design tools are standardizing")

## Related Skills

- **creative-research** — Use AFTER deep-research. Divergence, constraint discovery, cross-domain patterns.
- **brainstorming** — Use AFTER both deep-research and creative-research. Recon with your findings.

