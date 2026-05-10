# Test Plan: Claude Creative Skills

## Test Scenarios

**Skill Order**: `/michael:deepresearch` → `/michael:brainstorming` → `/michael:executeplan`

### Scenario 1: Deep Research (Realistic Pressure Test)

**Prompt**: "Research vertical SaaS adoption in legal tech. Why are vertical legal SaaS tools winning vs. horizontal legal practices management systems?"

**Success Criteria**:
- ✓ Recon pass evident (identified scope, assumptions listed)
- ✓ Depth-2 decomposition clear (3-5 subquestions with Level 2 dives)
- ✓ Parallel subagent structure callable (can see parallelism)
- ✓ Confidence bands used (well-established, contested, low-confidence)
- ✓ Adversarial pass attempted (searched for contradictions)
- ✓ Positioning gap identified (something competitors miss)

**Expected output**: ~2000-3000 words; 5-7 sources per finding; 3 positioning gaps

---

### Scenario 2: Brainstorming (Realistic Pressure Test)

**Prompt** (pre-supplied research): 
```
Deep-research findings:
- Vertical legal SaaS growing 25% YoY vs. horizontal 8% YoY
- Compliance + integrations are key differentiation
- Adoption barrier: long sales cycles (9-12 months for enterprise deals)

Real decision: We're building a legal tech product for small law firms. 
Should we target solo practitioners, small firms (2-10 people), or mid-market (10-50 people)?

Generate 2-3 worldview-axis approaches with real tradeoffs.
```

**Success Criteria**:
- ✓ Decision reframed (what's actually at stake?)
- ✓ 2-3 worldview approaches generated (not generic features)
- ✓ Approaches have real tradeoffs (not all positive)
- ✓ Adversarial thinking applied (reframe, premortem, red-team)
- ✓ One winner recommended with confidence level

**Expected output**: 3 approaches (500 words each); adversarial findings documented; recommendation with confidence signal

---

### Scenario 3: Execute-Plan (Realistic Pressure Test)

**Prompt** (with research findings from Scenarios 1+2):
```
Strategy brief: We're building a legal tech product for small law firms.

Research:
- Deep-research shows vertical SaaS winning on compliance + integrations
- Creative-research identified precedents: Stripe (owned payments for SMBs), Zapier (no-code automation), Slack (communication tool that became essential)

Real decision: Should we target solo practitioners, small firms (2-10 people), or mid-market (10-50 people)?

Generate 2-3 worldview-axis approaches with real tradeoffs. Run adversarial pre-pass.
```

**Success Criteria**:
- ✓ Recon pass evident (constraints listed, real decision framed)
- ✓ 2-3 worldview axes generated (not generic features)
- ✓ Approaches have tradeoffs (not all positive)
- ✓ Multi-choice questions bundled (real-world precedents cited)
- ✓ 3 adversarial checkpoints run (reframe, premortem, red-team)
- ✓ No lists of ideas (coherent approaches only)

**Expected output**: 3 approaches (500 words each); adversarial findings documented; recommendation with confidence signal

---

### Scenario 4: Execute Plan (Realistic Pressure Test)

**Prompt** (spec from Scenario 2 brainstorming):
```
Spec: Develop landing page for legal tech product (small law firm focus).

Brief:
- Positioning: "Compliance + integrations for small law firms, so you can focus on cases"
- CTA: "Start 14-day free trial"
- Target: Solo practitioners + small law firms on Google + Indie Hackers

Deliverables:
1. Landing page copy (headline + 3 sections + CTA)
2. Visual design mockup (hero image description + layout)
3. Integration checklist (which law-specific tools to integrate)

Acceptance: Spec-compliant, copyedit-ready, brand-aligned
```

**Success Criteria**:
- ✓ Spec review done (ambiguity flagged)
- ✓ Decomposed into 3-4 independent tasks
- ✓ Each task has clear acceptance criteria
- ✓ Blockers escalated (Tier 1 → Tier 2 → user decision structure evident)
- ✓ Confidence signals used (🟢 Green / 🟡 Yellow / 🔴 Red)
- ✓ Smoke gate passed (no hallucinated APIs, no TODOs, copyedit clean)
- ✓ PROGRESS.md audit trail documented

**Expected output**: Landing page copy + mockup + integration checklist; 1-2 blockers handled; all confidence signals green

---

## Test Execution Order

1. Run Scenario 1 (michael:deepresearch)
2. Run Scenario 2 (michael:brainstorming) using Scenario 1 output
3. Run Scenario 3 (michael:executeplan) using Scenario 2 output

This end-to-end flow tests skill composition: deepresearch → brainstorming → executeplan.

**Total end-to-end time**: ~60 minutes

---

## Evaluation Metrics

| Skill | Success Rate | Token Efficiency | Output Quality |
|-------|--------------|------------------|-----------------|
| michael:deepresearch | Need ≥5/6 criteria | <25K tokens | Fact-grounded, sources cited, confidence bands applied |
| michael:brainstorming | Need ≥5/6 criteria | <20K tokens | Real tradeoffs, not lists, adversarial thinking evident |
| michael:executeplan | Need ≥6/7 criteria | <30K tokens | Spec-compliant, no hallucinations, smoke gates verified |

---

## Iteration Plan (If Issues Found)

- **If deep-research lacks confidence bands**: Revise SKILL.md to require explicit "well-established / contested / low-confidence" labeling in JSON output
- **If creative-research precedents are too similar**: Add "must be from 3+ different domains" to SKILL.md
- **If brainstorming returns lists**: Revise to explicitly forbid "Ideas:" section; require "Approach A:", "Approach B:" format
- **If execute-plan has hallucinations**: Strengthen anti-hallucination guards in SKILL.md; add import verification checklist

