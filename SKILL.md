---
name: choose-effort
description: Recommends reasoning effort and an execution mode before heavy work in Claude Code or Codex, with setup instructions and a usage checkpoint. Use when the user asks which effort level to use, what the orchestrator level is, when to use Ultra, how to use less going forward, or how to set up a long run with subagents, goal mode, workflows, or agent teams. Not for past usage drains, persistent model tiers, plan limits, prices, or model support. Use diagnose-usage for past drains, setup-claude-advisor for persistent model tiers, and official product docs for plan limits, prices, or model support.
version: 1.1.0
---

# Choose effort

Recommend a reasoning level, a way to run the task, and a first checkpoint. The user applies any setting changes.

## Workflow

1. Identify the host and client from the session. If unclear, ask whether the user is in Claude Code, the Codex app, or the Codex CLI.
2. Ask up to three short questions about task scope, the cost of a wrong answer, and usage constraints. Skip anything the user already told you. If they only ask for a definition, such as which Codex setting orchestrates subagents, answer directly.
3. Choose a starting level from the table. Use the labels available in the user's model and client. If unsure, point to the picker or check current product docs.
4. Choose an execution mode based on whether the work can be split. Use the host-specific guidance below.
5. Give the recommendation, how to set it, and when to check progress and usage. Only report a setting change after the user or client confirms it.

| Task | Start at |
|---|---|
| Rename, summarise, small scoped edit | Low |
| Normal feature work | Medium or the model default |
| Hard debugging, design, large refactor | High |
| Production-critical work where high already fell short | Extra high, where available |
| One-off hardest problem | Highest available single-agent effort, if the added time and usage are worthwhile |

### Codex

- **Ultra mode** is the Codex option for proactive subagent orchestration where the client and model offer it. Recommend it for larger tasks with independent work, such as investigating separate modules or reviewing different risks. Use a regular effort level for tightly coupled work that benefits from shared context. High, Extra high, and Max are reasoning levels.
- For a specific split, the user can explicitly request subagents where supported. Give each agent a distinct question or file scope. Use goal mode (`/goal` where available) for persistence toward a clear outcome. A goal can use one agent or several.
- In the app, use the model and reasoning controls below the composer or `/reasoning` where available. In the CLI, use `/model` to see supported options. For example, use `/model --reasoning=high` if the active model supports it. Recommend Ultra through the available mode picker when it appears.
- Check progress after the first investigation or work split. Use `/status` for session information and `/usage` for usage where available.
- References: [Models and reasoning controls](https://learn.chatgpt.com/docs/models?surface=app#choose-a-model), [subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents), [app slash commands](https://learn.chatgpt.com/docs/app/slash-commands), and [CLI model picker](https://learn.chatgpt.com/docs/developer-commands?surface=cli#set-the-active-model-with-model).

### Claude Code

- Use `/effort <level>`, or `claude --effort <level>` for one launched session. Check the confirmation text because `/effort` may save the new default. Use `/effort auto` to clear it. If unsure which levels are supported, ask the user to check the `/effort` slider.
- Subagents inherit the session's effort by default. For mechanical fan-out, recommend a lower session level and a first checkpoint. Call out any planned subagents, Agent Teams, workflows, `/goal`, or long SDK run.
- Check `/usage` after the first stage and at the end. Route a past usage drain to `diagnose-usage`. Route plan allowances, prices, and model support to `product-self-knowledge`.

## Hand off

- Send a completed run's usage question to `diagnose-usage`.
- Send a request for persistent advisor or subagent model tiers to `setup-claude-advisor`.

## Answer shape

- **Task** — scope and cost of getting it wrong.
- **Effort** — the recommended level and why.
- **Execution** — one agent, scoped subagents, or an available orchestration mode. Include goal mode if persistence matters.
- **Setup** — the exact control for this host and client.
- **Checkpoint** — what to check and when.

See `references/trigger-cases.md` when tuning the skill's trigger.
