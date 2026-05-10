# Deployment Guide: Claude Creative Skills

## Installation

### Option 1: Local Development (Recommended)

Copy skills to your Claude plugins directory:

```bash
cp -r . ~/.claude/skills/
```

Or, if you use a different skills directory:

```bash
cp -r . /path/to/your/claude/skills/
```

### Option 2: Clone from GitHub

```bash
git clone https://github.com/fortun8te/claude-creative-skills.git ~/.claude/skills/creative-skills
```

Then verify skills are discoverable in your Claude client.

---

## Verification

After installation, test skill discovery:

### In Claude Code CLI

```bash
/skill michael:deepresearch
```

Should print the skill metadata + description.

### In Claude Web / Desktop

Open any conversation. Type `/` and look for:
- `/michael:deepresearch`
- `/michael:brainstorming`
- `/michael:executeplan`

Skills should appear in autocomplete.

---

## First Use: End-to-End Test

Follow the four-scenario test plan in `TEST_PLAN.md`:

1. **Scenario 1: Deep Research** (~15 min)
   - Prompt: Research a market topic (e.g., "Research vertical SaaS adoption in legal tech")
   - Verify: Recon pass, Depth-2 decomposition, confidence bands, adversarial pass

2. **Scenario 2: Creative Research** (~12 min)
   - Use output from Scenario 1 as input
   - Prompt: Find cross-domain precedents, extract positioning principles
   - Verify: 5+ precedents, positioning gaps, divergence pass

3. **Scenario 3: Brainstorming** (~15 min)
   - Use outputs from Scenarios 1+2 as input
   - Prompt: Generate 2-3 worldview-axis approaches
   - Verify: Tradeoffs, multi-choice questions, adversarial thinking

4. **Scenario 4: Execute Plan** (~20 min)
   - Use output from Scenario 3 as input
   - Prompt: Execute the spec into deliverables
   - Verify: Task decomposition, blockers escalation, smoke gates

**Total end-to-end time**: ~60 minutes

---

## Skill Philosophy

Each skill is designed for **depth without bloat**:

- **michael:deepresearch**: Parallel subagents + adversarial verification (combines fact-finding + positioning discovery, cheaper than manual research, more thorough than single LLM pass)
- **michael:brainstorming**: Worldview approaches + adversarial thinking (prevents groupthink, surfaces real tradeoffs, picks one winner)
- **michael:executeplan**: Per-task subagents + runtime verification (prevents hallucination, ensures real delivery, smoke gates at every stage)

Use them in sequence: **michael:deepresearch → michael:brainstorming → michael:executeplan**

---

## Token Economy Tips

### Reduce Token Burn

1. **Cache research findings**: After deep-research, save findings to a shared doc or IndexedDB. Reference it in creative-research + brainstorming.

2. **Use cheap models for workers**: If you have access to model selection (e.g., in your own infrastructure):
   - Workers (subagents): Use 0.8b–2b parameter models
   - Synthesis: Use 4b–9b parameter models

3. **Hard iteration caps**: Each skill has built-in caps:
   - michael:deepresearch: Max 5 research angles, max 30 min total, parallel agent orchestration
   - michael:brainstorming: Max 3 worldview approaches, 1 adversarial pass (reframe/premortem/red-team)
   - michael:executeplan: Max 2 Tier 2 escalations per task, smoke gates at each stage

4. **Reuse across projects**: The research findings from one project can inform strategy in related projects. Copy findings to your notes/wiki.

---

## Customization

### Adapt Skills to Your Domain

Each skill is text-based and designed to be flexible. You can:

1. **Adjust scope**: Deep-research default is Depth-2. Increase to Depth-3 for highly specialized domains (e.g., quantum research). Decrease to Depth-1 for quick sprints.

2. **Swap precedent domains**: Creative-research looks for cross-domain precedents. If you're in B2B SaaS, you might prioritize precedents from:
   - Enterprise sales (long cycles)
   - Luxury goods (premium positioning)
   - Communities (retention)
   
   Adjust the skill to emphasize domains relevant to you.

3. **Add domain-specific acceptance criteria**: Execute-plan requires acceptance criteria. Adjust to match your domain:
   - **Code**: "Smoke gate passes (dev runs, console clean)"
   - **Content**: "Human read, no typos, on-brand tone"
   - **Campaign**: "All assets render, copy on-target"

---

## Troubleshooting

### Skills Not Appearing in Autocomplete

1. Restart Claude client
2. Check skill files are in `~/.claude/skills/` (verify `SKILL.md` files exist)
3. Run `ls -la ~/.claude/skills/*/SKILL.md` to verify paths

### Subagent Dispatch Errors (If Using Parallel Agents)

- Verify Claude Code or your agent framework supports parallel subagent dispatch
- If not, adapt skills to sequential dispatch (run one subagent at a time)

### Output Quality Issues

Refer to `TEST_PLAN.md` evaluation metrics. If a skill underperforms:
1. Check the success criteria (what specifically failed?)
2. Re-read the relevant SKILL.md section
3. Adjust the skill prompt (small tweaks often fix issues)
4. Log the issue in GitHub (we iterate on feedback)

---

## Contributing / Feedback

Issues, suggestions, or improvements?

1. Open an issue: https://github.com/fortun8te/claude-creative-skills/issues
2. Fork the repo and submit a PR with improvements
3. Tag us in discussions about how you're using the skills

---

## Version

- **Release**: 1.0 (May 2026)
- **Last Updated**: 2026-05-10
- **Repository**: https://github.com/fortun8te/claude-creative-skills

---

## Credits

Inspired by:
- **Rick Rubin** — Simplification, constraint as creativity driver
- **Anthropic's multi-agent research** — Parallel orchestration patterns
- **Superpowers skillset** — Structural patterns (brainstorming, execution)
- **Creative practitioners** — Sagmeister, Paula Scher, Working Backwards (Amazon)

Built for deep creative strategy work.

