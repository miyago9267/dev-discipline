# dev-discipline

Spec-Driven Development toolkit for Claude Code -- SDD/TDD workflows, agents, session management, and production-hardened rules.

## Install

### Claude Code (recommended)

```bash
# Add as marketplace source
claude plugin marketplace add miyago9267/dev-discipline

# Install
claude plugin install dev-discipline
```

Or load directly for a single session:

```bash
claude --plugin-dir /path/to/dev-discipline
```

### Other AI tools

```bash
git clone https://github.com/miyago9267/dev-discipline.git
cd dev-discipline
bash install.sh
```

Supports: Claude Code, Codex, Gemini, Cursor, Copilot.

### Project setup

Set up SDD v2 structure (`AGENTS.md` + `docs/specs/` + `.ai/`) in any project:

```bash
bash install.sh --project /path/to/project
```

## What's included

### Skills (15)

| Skill | Always On | Description |
|-------|-----------|-------------|
| sdd | | Spec-Driven Development v2 workflow |
| tdd | | Test-Driven Development (Red-Green-Refactor) |
| auto-spec | yes | Auto spec tracking and progress management |
| auto-docs | yes | Auto documentation to `.ai/` directory |
| efficiency | yes | Token/time efficiency discipline |
| markdown-lint | yes | markdownlint auto-fix on write |
| project-map | yes | Read `.ai/PROJECT.md` at session start |
| safe-ops | yes | Confirm before dangerous operations |
| path-aware | yes | Verify tool existence before claiming unavailable |
| no-ai-attribution | yes | No Co-Authored-By in commits |
| git-workflow | yes | Git safety rules and commit format |
| code-review | | Code review checklist |
| cicd-watch | | CI/CD pipeline monitoring |
| docker-k8s | | Docker and Kubernetes dev guide |
| strategic-compact | | Suggest `/compact` at logical breakpoints |

### Agents (8)

| Agent | Description |
|-------|-------------|
| code-reviewer | Code quality, security, performance review |
| debugger | Systematic debugging and root cause analysis |
| researcher | Tech research before implementation |
| spec-writer | Create and maintain SDD specs |
| planner | Break specs into implementation steps |
| tdd-guide | Enforce Red-Green-Refactor cycle |
| refactorer | Safe refactoring under test protection |
| cicd-watcher | Monitor and auto-fix CI/CD pipelines |

### Commands (17)

| Command | Description |
|---------|-------------|
| `/sdd` | Start or continue SDD workflow |
| `/plan` | Design implementation plan before coding |
| `/verify` | Run build/type-check/lint/test pipeline |
| `/handoff` | Export session state for next session |
| `/pickup` | Resume from previous session's handoff |
| `/build-fix` | Incrementally fix build errors |
| `/test-coverage` | Analyze and improve test coverage |
| `/refactor-clean` | Remove dead code safely |
| `/checkpoint` | Save/verify work progress |
| `/e2e` | Playwright end-to-end testing |
| `/eval` | Evaluation-driven development |
| `/learn` | Extract reusable patterns from session |
| `/rev-doc` | Reverse engineering documentation |
| `/orchestrate` | Multi-agent workflow orchestration |
| `/update-codemaps` | Update architecture maps |
| `/update-docs` | Sync documentation from package.json |
| `/init-ai-dir` | Initialize `.ai/` in a project |

### Hooks (2)

- **PostToolUse (Write/Edit)**: Auto-format (biome/prettier/gofmt/ruff/rustfmt) + markdown-lint
- **PreToolUse (Edit/Write)**: Strategic compact threshold reminder

### Rules (2)

- **sdd-tdd-rules**: Hard rules for SDD + TDD workflow
- **reverse-engineering**: Methodology for analyzing minified/obfuscated code

### Scripts (10)

Session management scripts for the SDD v2 two-layer architecture:

| Script | Description |
|--------|-------------|
| `bootstrap.sh` | New session bootstrap (read handoff/changelog/specs) |
| `check.sh` | Health check, `--init` to initialize `.ai/` |
| `log.sh` | Append changelog entry |
| `lesson.sh` | Record lessons learned |
| `snapshot.sh` | Save/restore mid-session checkpoints |
| `end-session.sh` | End session (CURRENT -> HANDOFF + summary) |
| `spec-archive.sh` | Archive completed batch/phase |
| `skill-create.sh` | Create new skill files |
| `ai-export.sh` | Export `.ai/` to `docs/ai/` for git |
| `knowledge-sync.sh` | Sync knowledge base |

### Templates (5)

- `SPEC.template.md` -- Spec with ADR, alternatives, rabbit holes
- `TASKS.template.md` -- Batch task checkboxes
- `TESTS.template.md` -- EARS syntax acceptance criteria
- `PROGRESS.template.md` -- Phase-level tracking
- `AGENTS.md` -- Cross-tool project rules (SDD/TDD/efficiency)

## Architecture: Two-Layer Separation

```text
Spec layer (always committed):
docs/specs/<slug>/
  SPEC.md      -- What + Why + ADR
  TASKS.md     -- Current batch checkboxes
  TESTS.md     -- EARS acceptance criteria
  PROGRESS.md  -- Phase tracking
  archive/     -- Completed work

Working memory (always gitignored):
.ai/
  CURRENT.md   -- Current session state
  HANDOFF.md   -- Cross-session handoff
  changelog.md -- Operation log
  lessons.md   -- Lessons learned
```

## Companion plugins

- [ask-tty](https://github.com/miyago9267/ask-tty) -- stdin proxy for Claude Code (sudo, ssh, interactive input via Telegram)

## License

MIT
