# infiniteleverage-plugin — retired

> 🪦 **Retired and archived (2026-09-28).** This was the v1 Infinite Leverage plugin (the
> 8-agent system). It gets no further changes. Everything now lives in one repo:
> **https://github.com/edge8-ai/infinite-leverage** — the v2 plugin, its 4 agents, their
> skills and the project scaffold.

The files stay here, read-only, so nothing that still points at this repo breaks. Don't
install from it.

## Moving to v2

v1 and v2 use the same names (`infiniteleverage@infiniteleverage`), so remove v1 first:

```bash
claude plugin uninstall infiniteleverage@infiniteleverage
claude plugin marketplace remove infiniteleverage
```

Then install v2:

```bash
claude plugin marketplace add edge8-ai/infinite-leverage
claude plugin install infiniteleverage@infiniteleverage
```

v2 installs nothing machine-wide. The agents go into each project: run `/il-adopt` in an
existing repo or `/il-project` for a new one, restart Claude Code, then run `/il-doctor`.

**Edge8 machines:** v1's `init` and `patch` copied agents, skills, hooks, rules and a
`Bash(*)` permission grant into `~/.claude/`. Uninstalling the plugin does not remove
those copies — the private `edge8-telemetry` plugin does, on its first run.

## What changed

| v1 (here) | v2 |
|---|---|
| 8 agents, installed globally into `~/.claude/agents/` | 4 agents (product-manager, developer, qa, devops), installed per project |
| `/infiniteleverage-init`, `-onboard` | Install the plugin; nothing to set up on the machine |
| `/infiniteleverage-patch` | Marketplace updates; projects refresh with `/il-adopt` |
| `/infiniteleverage-validate` | `/il-doctor` |
| `/infiniteleverage-project` | `/il-project` |
| SessionStart / Stop hooks, telemetry | No hooks; telemetry moved to the private `edge8-telemetry` plugin |

Why v1 was replaced: this repo was a hand-copied snapshot of the template repo's
`setup-skills/`. The copies drifted, and `hooks.json` pointed at `~/.claude/hooks/*`
instead of `${CLAUDE_PLUGIN_ROOT}`, so plugin updates never took effect without a manual
copy step. v2 ships the plugin straight from the canonical repo.

The `edge8-ai/infiniteleverage-8-plugin` mirror mentioned in older notes is **not**
retired: it now distributes v2 to the claude.ai org plugin directory.
