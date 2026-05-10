# Claude Creative Skills

A 4-skill system for deep creative strategy work. Inspired by Rick Rubin, designed for token economy and real-world execution.

## Skills

1. **deep-research** — Parallel web research with orchestrator + subagents. Adversarial verification, confidence bands, depth-2 decomposition.
2. **creative-research** — Cross-domain constraint-driven research. Divergence-first, positioning, creative positioning gaps.
3. **brainstorming** — Recon pass before questions. Worldview-axis approaches. Adversarial pre-pass (reframe/premortem/red-team).
4. **execute-plan** — Per-task fresh-subagent review. Runtime smoke gates (dev + browser + clean console). Three-tier blocker escalation.

## Installation

Copy into your Claude config:

```bash
cp -r . ~/.claude/skills/
```

## Usage

Invoke any skill in Claude Code:

```
/invoke deep-research
/invoke creative-research
/invoke brainstorming
/invoke execute-plan
```

## Philosophy

- **Depth without bloat**: Parallel orchestration for wall-clock efficiency.
- **Token economy**: Cheap models for workers, strong models for synthesis.
- **Real-world execution**: Runtime smoke gates, staged verification, confidence-gated autonomy.
- **Adversarial thinking**: Reframe, premortem, red-team.
- **No yap**: TLDRs, not lists.

