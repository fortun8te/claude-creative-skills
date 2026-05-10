# Claude Creative Skills

A 3-skill system for deep creative strategy work. Inspired by Rick Rubin, designed for token economy and real-world execution.

## Skills

1. **michael:deepresearch** — Unified fact-finding + positioning discovery. Parallel research agents, confidence bands (well-established/contested/low-confidence), adversarial verification. Returns actionable insights.
2. **michael:brainstorming** — Convert research into 2-3 real approaches with tradeoffs. Adversarial thinking (reframe/premortem/red-team). Pick one winner with confidence level.
3. **michael:executeplan** — Ship strategy into reality. Spec → task decomposition → per-task subagent dispatch → spec compliance review → quality review → smoke gate → ship. Confidence signals (🟢/🟡/🔴), blocker escalation.

## Installation

Copy into your Claude config:

```bash
cp -r . ~/.claude/skills/
```

## Usage

Invoke any skill in Claude Code:

```
/michael:deepresearch
/michael:brainstorming
/michael:executeplan
```

## Philosophy

- **Depth without bloat**: Parallel orchestration for wall-clock efficiency.
- **Token economy**: Cheap models for workers, strong models for synthesis.
- **Real-world execution**: Runtime smoke gates, staged verification, confidence-gated autonomy.
- **Adversarial thinking**: Reframe, premortem, red-team.
- **No yap**: TLDRs, not lists.

