# choose-effort

An agent skill that automatically uses the active Claude Code or Codex client. Before a heavy run, it recommends how much reasoning
to use, whether the work should be split across agents, which control to use, and when to check
progress and usage. You apply the setting.

In Codex, **Ultra mode** can proactively bring in subagents when the client and model offer it.
Use it for work with independent parts. For a tightly coupled task, choose a reasoning level using
the app's reasoning control or the CLI's `/model` picker. In Claude Code, use `/effort`.

For a past Claude Code usage drain, use [diagnose-usage](https://github.com/arm-pz/diagnose-usage).

## Install

```
npx skills add arm-pz/choose-effort --skill choose-effort
```

Or copy the repo files into `~/.claude/skills/choose-effort/` for Claude Code or
`~/.agents/skills/choose-effort/` for Codex.

## Ask it things like

- "Which Codex level is the orchestrator?"
- "Should I use Ultra or High to debug this issue in Codex?"
- "What effort should I use in Claude Code to refactor the auth module?"
- "Set me up to run this overnight without burning through my limit."

## Validation

`references/trigger-cases.md` records a manual review of the expected triggers and boundaries.
It does not measure live skill activation.

## License

MIT — see [LICENSE](LICENSE).
