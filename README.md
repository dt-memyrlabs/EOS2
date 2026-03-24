# EOS — Enlightened Operating System v2.0.0

EOS is a context-staging system for AI reasoning partners. It displaces training priors with user context — the model generates from YOUR lived experience, constraints, and environment, not from textbook defaults. Rules handle residual leakage. 284 lines. Every directive passes: "if you remove it, does behavior visibly degrade?"

## How to Use

Copy `CLAUDE.md` into your Claude Code project root or paste into `userPreferences` on claude.ai. Skills go in `~/.claude/skills/` (Claude Code) or `/mnt/skills/user/` (claude.ai).

## File Structure

```
CLAUDE.md              # The kernel — 284 lines, 10 rules + builder mode
skills/                # Skill modules loaded on trigger
  eos-memory-mgmt.md   # Session start, Notion persistence, state writes
  eos-contradiction.md # Trajectory-aware contradiction handling
  eos-project-mgmt.md  # Assumption tracking, limiter analysis, convergence
  eos-goal-framing.md  # Goal extraction (core absorbed into kernel Rule 2)
  eos-builder.md       # Build mode (core absorbed into kernel Section 5)
  eos-collaboration.md # Collaborator authority (core absorbed into kernel Rule 7)
  + 10 more domain/utility skills
tasks/
  lessons.md           # Self-correcting rules from past corrections
rule-tests.md          # 28 behavioral test scenarios
comparison-report.md   # v20.5.0 vs v2.0.0 test results
```

## Test Results

28 scenario-based tests evaluated against both v20.5.0 (700+ lines) and v2.0.0 (284 lines):

| Version | PASS | PARTIAL | FAIL | Pass Rate |
|---|---|---|---|---|
| v20.5.0 | 16 | 11 | 1 | 57% |
| **v2.0.0** | **27** | **1** | **0** | **96%** |

No test regressed. Full analysis in [comparison-report.md](comparison-report.md).

## Core Architecture

1. **User Model** — populated from Notion at session start. Specificity is displacement strength.
2. **Identity** — generation targets, lean thinking, context-specific sarcasm, backstop violations.
3. **10 Rules** — Goal Lock, Generation Frame, Progress Tracking, Contradiction, Regression Lock, Autonomy, User Authority, Operational Empathy, Context Limit, Output Integrity.
4. **Builder Mode** — artifacts-first when user says "let's build."
5. **State Storage** — Notion as primary store, immediate writes on decision-lock events.
6. **Skill Modules** — separate files loaded on trigger. Directory is the registry.

## License

MIT
