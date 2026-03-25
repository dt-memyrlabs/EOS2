# EOS 2

A system prompt that makes Claude think from your context instead of its training data.

## What it does

When you ask Claude for advice, it defaults to textbook answers. EOS changes that. It makes Claude generate from your actual situation — your constraints, your experience, your tools — instead of generic best practices.

It also makes Claude honest. There's a truth gate that runs before every response: "Is this actually true, or does it just look complete?" If Claude can't prove something, it says so before presenting it.

## How it works

`CLAUDE.md` is a 300-line file that goes in your project root. It has:

- **Your context first.** Claude reads your background before anything else. The more specific you are, the less generic the output.
- **10 rules.** Things like: don't start working until the goal is clear. When multiple paths exist, test them all and recommend the best one. If you challenge a recommendation, don't cave unless there's a real argument — pushback alone isn't enough.
- **A truth gate.** Before every response: Is this true? What can't I prove? Am I producing this because it was asked for, or because it's right?
- **Plain language.** If a 15-year-old can't follow the explanation, rewrite it.
- **Skills.** Separate files that handle specific workflows (project management, memory, contradiction tracking). They load when needed.

## Setup

**Claude Code:** Drop `CLAUDE.md` in your project root. Put skill files in `~/.claude/skills/`.

**claude.ai:** Paste `CLAUDE.md` content into your project's custom instructions. Upload skills to `/mnt/skills/user/`.

## What's in the repo

- `CLAUDE.md` — the kernel. This is the thing that changes behavior.
- `skills/` — 16 workflow modules that load on trigger.
- `rule-tests.md` — 28 test scenarios that prove each rule does something observable.
- `comparison-report.md` — EOS 2 vs the previous version (v20.5.0, 700+ lines). The old one was so long that Claude stopped paying attention to the important parts. This one is short enough that every rule actually gets read.

## License

MIT
