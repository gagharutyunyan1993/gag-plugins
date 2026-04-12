# Claude Dev Pack

A complete dev workflow plugin for Claude Code. 20 prefixed skills covering planning, implementation, review, debugging, testing, git operations, and session management.

## What It Does

Encodes a structured development workflow into reusable skills with category prefixes:

- **`do-` Actions** — plan, spec, build, fix, diagnose, review. Core development loop from planning through code review
- **`be-` Modifiers** — deep, fast, safe, minimal, rewrite. Stack on top of any action to change behavior (deeper analysis, tighter scope, safer changes)
- **`run-` Orchestration** — agents, r1, l2. Multi-role pipelines and iterative improvement passes
- **`git-` Git ops** — commit, pr. Conventional commits and pull requests with auto-generated descriptions
- **`use-` Utilities** — test, explain. Test generation that reads existing patterns first, code explanation with diagrams
- **`ses-` Sessions** — start, end. Persist context across sessions via handoff notes

## Key Features

- **Frontmatter-driven** — `effort`, `model`, `context: fork`, `allowed-tools`, `disable-model-invocation` configured per skill
- **Dynamic context** — skills inject `git diff`, `git log`, `git status` so Claude starts with real project state
- **OODA debugging** — `do-fix` uses Observe-Orient-Decide-Act loop for root cause analysis
- **Severity-based review** — `do-review` categorizes findings as CRITICAL / WARNING / SUGGESTION
- **Opus for critical tasks** — `do-review` and `do-spec` auto-select `claude-opus-4-6`
- **Isolated review** — `do-review` and `run-agents` use `context: fork` for independent assessment
- **4-role pipeline** — `run-agents` runs Planner → Engineer → Tester → Reviewer via `Task()` subagents
- **ultrathink** — `be-deep` activates extended reasoning budget
- **Manual-only git actions** — `git-commit` and `git-pr` require explicit invocation
- **Shell-neutral** — no bash-specific syntax; works across platforms

## Usage

```
/claude-dev-pack:do-plan add OAuth2 authentication
```

Plan before implementation. Reads git history and relevant code first.

```
/claude-dev-pack:do-fix null pointer in UserService
/claude-dev-pack:be-safe
```

OODA bug fix with conservative, regression-aware approach.

```
/claude-dev-pack:do-review
```

Strict code review on Opus with severity levels, running in isolated context.

```
/claude-dev-pack:run-agents design a caching layer
```

4-role pipeline with full context isolation between roles.

```
/claude-dev-pack:git-commit
```

Conventional commit from current diff.

```
/claude-dev-pack:ses-start
/claude-dev-pack:ses-end
```

Load previous session context / write handoff notes.

## Install

### Local development / testing

```bash
claude --plugin-dir /path/to/claude-dev-pack
```

This is the recommended way to test the plugin locally while iterating on it. After edits, run `/reload-plugins` inside Claude Code to pick up changes without restarting.

### Persistent/shared installation

Install through the `gag-plugins` marketplace:

```text
/plugin marketplace add gagharutyunyan1993/gag-plugins
/plugin install claude-dev-pack@gag-plugins
```

## Skills Reference

### Actions (`do-`)

| Skill | Description | Frontmatter |
|---|---|---|
| `do-plan` | Implementation plan before code | `effort: high` |
| `do-spec` | Formal technical specification | `effort: max`, `model: claude-opus-4-6` |
| `do-build` | Implement with test + lint verification | `effort: high`, `allowed-tools` |
| `do-fix` | OODA bug fix, root cause focus | `effort: high` |
| `do-diagnose` | Hypothesis-driven investigation | `effort: high` |
| `do-review` | Strict review with severity levels | `model: claude-opus-4-6`, `context: fork` |

### Modifiers (`be-`)

| Skill | Description | Frontmatter |
|---|---|---|
| `be-deep` | Multi-approach analysis + ultrathink | `effort: max` |
| `be-fast` | Smallest useful pass, skip discussion | `effort: low` |
| `be-safe` | Conservative changes, regression-aware | `allowed-tools` (pre-approved inspection tools) |
| `be-minimal` | Scope cap: stop if >3 files | — |
| `be-rewrite` | Broad restructuring with guardrails | `disable-model-invocation` |

### Orchestration (`run-`)

| Skill | Description | Frontmatter |
|---|---|---|
| `run-agents` | Planner→Engineer→Tester→Reviewer | `effort: max`, `context: fork` |
| `run-r1` | One review-and-fix iteration | — |
| `run-l2` | Two passes: correctness then quality | — |

### Git (`git-`)

| Skill | Description | Frontmatter |
|---|---|---|
| `git-commit` | Conventional commit from diff | `disable-model-invocation`, `allowed-tools: [Bash(git *)]` |
| `git-pr` | PR with auto description + review | `disable-model-invocation`, `allowed-tools: [Bash(git *), Bash(gh *)]` |

### Utilities (`use-`)

| Skill | Description | Frontmatter |
|---|---|---|
| `use-test` | Tests matching existing patterns | `effort: high` |
| `use-explain` | Explain with analogies + diagrams | `effort: low` |

### Sessions (`ses-`)

| Skill | Description | Frontmatter |
|---|---|---|
| `ses-start` | Load previous session context | `effort: low` |
| `ses-end` | Write handoff to session-notes.md | `effort: low` |

## How Modifiers Work

Modifiers are invoked separately after an action skill. Claude sees both instruction sets via context accumulation:

```
/claude-dev-pack:do-build add /health endpoint
/claude-dev-pack:be-minimal
```

This is a workflow pattern — two separate invocations, not a combined syntax.

`be-safe` is a conservative workflow modifier, not a hard read-only sandbox. Its `allowed-tools` field pre-approves read-oriented inspection tools and git history/diff commands so Claude can inspect state with fewer prompts.

## License

MIT
