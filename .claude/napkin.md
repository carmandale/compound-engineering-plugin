# Napkin

## Corrections
| Date | Source | What Went Wrong | What To Do Instead |
|------|--------|----------------|-------------------|
| 2026-02-17 | Session | Skill duplicates existed in both `~/.pi/agent/skills/` and `~/.pi/agent/skills/compound/` | Only keep skills in `~/.agent-config/skills/compound/` - the symlinks handle distribution |
| 2026-02-17 | Session | Extension `compound-engineering-compat.ts` conflicted with native `pi-subagents` | Remove the extension - `pi-subagents` provides the native `subagent` tool |
| 2026-02-17 | Session | Gemini install with `-o ~/.gemini` created nested `.gemini/.gemini` | Gemini target auto-adds `.gemini/` - use parent dir or project dir |
| 2026-02-17 | Session | Plugin used `docs/plans/` but AGENTS.md requires `specs/<id>/` | Created fork with canonical paths - use `specs/<id>/plan.md` |

## User Preferences
- Uses `~/.agent-config` as unified config repo for all agents
- Prefers symlinks over copies for shared resources
- Wants single install command for all agents
- **Canonical planning structure**: `specs/<id>/` with spec.md, plan.md, tasks.md, research.md

## Patterns That Work
- `bunx @every-env/compound-plugin install compound-engineering --to opencode --also codex,droid,pi` for global targets
- `~/.agent-config/install.sh` for symlinks
- Combined `~/.agent-config/install-all.sh` for complete setup
- Fork for local customizations: `origin` = fork, `upstream` = EveryInc

## Patterns That Don't Work
- Installing same skill to multiple locations (causes conflicts)
- Custom extensions that duplicate native tool functionality
- Using `docs/plans/` - deprecated, use `specs/<id>/`

## Domain Notes
- **v0.9.0**: Added Kiro CLI target, renamed Cursor → Copilot (Cursor now uses native plugin)
- **Project-level targets**: copilot (.github/), gemini (.gemini/), kiro (.kiro/)
- **Global targets**: opencode, codex, droid, pi (user home directories)
- Skills are unified via `~/.agent-config/skills/` symlinked to all agents
- **Fork branch**: `feat/specs-canonical-paths` - aligns plan paths with AGENTS.md
