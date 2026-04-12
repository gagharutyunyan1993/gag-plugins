# Claude Dev Pack

![Skills](https://img.shields.io/badge/Skills-20-brightgreen?style=for-the-badge)
![Categories](https://img.shields.io/badge/Categories-6-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-purple?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-orange?style=for-the-badge)

> A structured Claude Code plugin that encodes a complete development workflow — from planning to deployment — into 20 prefixed skills with composable modifiers.

Built following [Anthropic's Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices) and community patterns from 10+ top repositories.

## Why This Plugin?

Most Claude Code setups use ad-hoc prompts that get lost between sessions. This plugin encodes **team-quality workflows** into reusable skills so you never re-explain your process.

**What makes it different:**

- **Action + Modifier pattern** — run `/do-fix` for a bug fix, then stack `/be-safe` for conservative mode. Mix and match any action with any modifier
- **Prefixed categories** — type `/do-` and autocomplete shows all actions. Type `/be-` for all modifiers. No memorization needed
- **Frontmatter-driven** — effort levels, model selection, context isolation, and tool permissions configured per skill — not buried in prompt text
- **Shell-neutral** — no `cat`, `find`, or bash-specific syntax. Works identically on Windows, macOS, and Linux
- **4-role AI pipeline** — Planner → Engineer → Tester → Reviewer with genuine context isolation via `Task()` subagents
- **Session persistence** — start and end sessions with automatic handoff notes that survive across conversations

## Install

```
/plugin marketplace add gagharutyunyan1993/gag-plugins
/plugin install claude-dev-pack@gag-plugins
```

That's it. All 20 skills are available immediately.

**For local testing:**
```bash
claude --plugin-dir /path/to/gag-plugins/plugins/claude-dev-pack
```

## Skill Categories

### `do-` Actions — Core Development Loop

| Skill | What it does | Key features |
|---|---|---|
| `do-plan` | Implementation plan before writing code | Reads git log + project structure first |
| `do-spec` | Formal technical specification | Runs on Opus, reads project manifest |
| `do-build` | Implement with verification | Auto-runs tests + linting after build |
| `do-fix` | OODA bug fix | Observe → Orient → Decide → Act → Verify |
| `do-diagnose` | Hypothesis-driven investigation | Logs findings to `.claude/debug.log` |
| `do-review` | Strict code review | Opus, isolated context, severity levels |

### `be-` Modifiers — Stack on Any Action

| Skill | Effect | Example combo |
|---|---|---|
| `be-deep` | Multi-approach analysis + ultrathink | `/do-fix` + `/be-deep` — deep root cause analysis |
| `be-fast` | Smallest useful pass, skip discussion | `/do-build` + `/be-fast` — quick implementation |
| `be-safe` | Conservative, regression-aware changes | `/do-fix` + `/be-safe` — careful bug fix |
| `be-minimal` | Scope cap: stop if >3 files touched | `/do-build` + `/be-minimal` — surgical change |
| `be-rewrite` | Broad restructuring with guardrails | `/do-build` + `/be-rewrite` — major refactor |

### `run-` Orchestration — Multi-Step Workflows

| Skill | What it does |
|---|---|
| `run-agents` | 4-role pipeline: Planner → Engineer → Tester → Reviewer (isolated via `Task()`) |
| `run-r1` | One review-and-fix iteration with optional focus area |
| `run-l2` | Two passes: correctness first, code quality second |

### `git-` Git Operations

| Skill | What it does |
|---|---|
| `git-commit` | Conventional commit from current diff (`feat:`, `fix:`, `refactor:`, ...) |
| `git-pr` | PR with auto-generated description + final review pass |

### `use-` Utilities

| Skill | What it does |
|---|---|
| `use-test` | Generate tests by reading existing test patterns first |
| `use-explain` | Explain code with analogies, ASCII diagrams, and gotchas |

### `ses-` Session Management

| Skill | What it does |
|---|---|
| `ses-start` | Load context from previous session notes |
| `ses-end` | Write handoff document to `.claude/session-notes.md` |

## Workflows

**Plan → Build → Review:**
```
/claude-dev-pack:do-plan add user authentication
/claude-dev-pack:do-build
/claude-dev-pack:do-review
```

**Safe bug fix with deep analysis:**
```
/claude-dev-pack:do-fix memory leak in worker pool
/claude-dev-pack:be-safe
/claude-dev-pack:be-deep
```

**Full AI pipeline:**
```
/claude-dev-pack:run-agents design a caching layer
```
Spawns 4 isolated roles — each works independently without seeing prior reasoning.

**Investigate → Fix → Review → Commit:**
```
/claude-dev-pack:do-diagnose flaky test in CI
/claude-dev-pack:do-fix
/claude-dev-pack:run-r1 edge cases
/claude-dev-pack:git-commit
```

**Quick minimal change:**
```
/claude-dev-pack:do-build add /health endpoint
/claude-dev-pack:be-fast
/claude-dev-pack:be-minimal
```

**Session continuity across conversations:**
```
/claude-dev-pack:ses-start          # load previous context
# ... work ...
/claude-dev-pack:ses-end            # save handoff notes
```

## How Modifiers Work

Modifiers are invoked **separately** after an action skill. Claude sees both instruction sets via context accumulation — this is a workflow pattern, not a combined syntax:

```
/claude-dev-pack:do-build add search feature    # action
/claude-dev-pack:be-safe                         # modifier: conservative
/claude-dev-pack:be-minimal                      # modifier: tight scope
```

All three instruction sets are active simultaneously. You can stack any number of modifiers on any action.

## Under the Hood

Each skill uses Claude Code's skills frontmatter system:

| Feature | How it's used |
|---|---|
| `effort: high/max/low` | Controls reasoning depth — `be-deep` sets `max`, `be-fast` sets `low` |
| `model: claude-opus-4-6` | `do-review` and `do-spec` auto-select the strongest model |
| `context: fork` | `do-review` and `run-agents` run in isolated subagent context |
| `allowed-tools` | `do-build` pre-approves Bash/Read/Write/Edit; `be-safe` pre-approves inspection and git diff/log tools |
| `disable-model-invocation` | `git-commit`, `git-pr`, `be-rewrite`, `run-agents` — manual only |
| `$ARGUMENTS` | `do-plan`, `do-spec`, `do-fix`, `run-r1`, `use-test`, `use-explain` accept parameters |
| `ultrathink` | `be-deep` activates extended thinking token budget |

## Project Structure

```
gag-plugins/
├── .claude-plugin/
│   └── marketplace.json
└── plugins/
    └── claude-dev-pack/
        ├── .claude-plugin/
        │   └── plugin.json
        └── skills/
            ├── do-plan/          ├── be-deep/
            ├── do-spec/          ├── be-fast/
            ├── do-build/         ├── be-safe/
            ├── do-fix/           ├── be-minimal/
            ├── do-diagnose/      ├── be-rewrite/
            ├── do-review/        ├── run-agents/
            ├── git-commit/       ├── run-r1/
            ├── git-pr/           ├── run-l2/
            ├── use-test/         ├── ses-start/
            └── use-explain/      └── ses-end/
```

## Contributing

Contributions welcome — new skills, improvements to existing ones, documentation, bug fixes.

1. Fork the repository
2. Add or modify skills in `plugins/claude-dev-pack/skills/`
3. Follow the prefix convention: `do-`, `be-`, `run-`, `git-`, `use-`, `ses-`
4. Keep SKILL.md under 500 lines (use supporting files for reference material)
5. Use affirmative instructions ("preserve existing logic" not "don't break things")
6. Submit a pull request

## Credits

Design informed by analysis of community best practices from [wshobson/claude-code-commands](https://github.com/wshobson/claude-code-commands), [qdhenry/Claude-Command-Suite](https://github.com/qdhenry/Claude-Command-Suite), [Anthropic's official plugin examples](https://github.com/anthropics/claude-code/tree/main/plugins), and [Anthropic's Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices).

## License

MIT
