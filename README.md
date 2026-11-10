# claude-model-router

A Claude Code skill that picks the right Claude model for each piece of work, so you stop
running everything on one.

Anthropic published a guide on which model to use for which task. Nobody is going to consult a
table before every prompt. This skill hands the table to Claude: the main session stays on your
model, and whenever it delegates to a subagent it picks the cheapest tier that will finish the
job. Haiku reads the logs, Sonnet makes the scoped edit, Fable plans the migration.

## What it does

- **Routes subagents by task type** (haiku / sonnet / opus / fable).
- **Never switches your main model mid-session**, because that throws away the prompt cache.
- **Escalates in the right order** when a result falls short: verify, then effort, then model.
- **Flags a clear mismatch** between your session's model and the task, in one line.

## Install

```bash
git clone https://github.com/Rajvardhman05/claude-model-router ~/.claude/skills/claude-model-router
```

Then add this to `~/.claude/CLAUDE.md` so the routing fires every time, not only when the skill
happens to load:

```markdown
## Model Routing

Before spawning any subagent, load the `claude-model-router` skill and set the subagent's model from
its routing table. Never switch the main session's model mid-task.
```

## Source

Rules are condensed from Anthropic's "Which Claude model should you build with?"
(https://claude.dev/blog/which-claude-model-should-you-build-with/, November 2026). Model tiers
and prices change; re-check the guide when a new generation ships.

## License

MIT
