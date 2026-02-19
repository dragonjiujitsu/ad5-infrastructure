# AD-5 Creative - Project Infrastructure

Repeatable project standards for every AD-5 repo. Install once, apply everywhere.

v1.1.0

## The Problem

Every new Claude Code session starts from zero. Standards like state.md, versioning, commit messages, and security rules live in Shawn's head. This infrastructure moves them into files that Claude Code reads automatically.

## How Claude Code Memory Works

Claude Code loads CLAUDE.md files from multiple locations in a hierarchy:

```
~/.claude/CLAUDE.md              Global. All projects, all sessions. YOUR standards.
~/.claude/settings.json          Global hooks. Run on every project.
~/.claude/commands/*.md           Global slash commands. Available everywhere.

project/.claude/CLAUDE.md        Project. Shared with team via git.
project/.claude/settings.json    Project hooks. Shared via git.
project/.claude/commands/*.md     Project slash commands. Shared via git.

project/CLAUDE.md                Alternative to .claude/CLAUDE.md (same effect).
project/CLAUDE.local.md          Personal. Auto-gitignored. Just you.
```

All files load automatically when Claude Code starts. Global first, then project. You never have to explain your standards. They're just there.

Source: https://code.claude.com/docs/en/memory and https://www.anthropic.com/engineering/claude-code-best-practices

## What's In This Repo

### Layer 1: Global (install on each machine)

| File | Installs To | Purpose |
|------|------------|---------|
| `global-claude/CLAUDE.md` | `~/.claude/CLAUDE.md` | AD-5 standards for every project |
| `global-claude/settings.json` | `~/.claude/settings.json` | Hooks that remind you to update state.md |
| `global-claude/commands/new-project.md` | `~/.claude/commands/new-project.md` | `/new-project` scaffolds a repo |
| `global-claude/commands/update-state.md` | `~/.claude/commands/update-state.md` | `/update-state` syncs state.md |
| `global-claude/commands/phase-gate.md` | `~/.claude/commands/phase-gate.md` | `/phase-gate` runs completion checklist |
| `global-claude/commands/handoff.md` | `~/.claude/commands/handoff.md` | `/handoff` generates session summary |

### Layer 2: Project Template (copy into each new repo)

| File | Purpose |
|------|---------|
| `project-template/.claude/CLAUDE.md` | Project-specific instructions (customize per project) |
| `project-template/.claude/settings.json` | Project hooks (TypeScript type check after edits) |
| `project-template/state.md` | State tracking template |
| `project-template/.gitignore` | Security entries for keys, env files, service accounts |
| `project-template/.gitattributes` | Line ending normalization, linguist overrides |
| `project-template/.env.example` | Environment variable template |

## Installation

### First Time Setup (once per machine)

```bash
# Clone this repo
git clone https://github.com/dragonjiujitsu/ad5-infrastructure.git
cd ad5-infrastructure

# Create ~/.claude if it doesn't exist
mkdir -p ~/.claude/commands

# Install global standards
cp global-claude/CLAUDE.md ~/.claude/CLAUDE.md
cp global-claude/settings.json ~/.claude/settings.json
cp global-claude/commands/*.md ~/.claude/commands/
```

Done. Every Claude Code session on this machine now knows AD-5 standards.

### New Project Setup

Option A: Use the /new-project command (recommended):
```bash
cd your-new-repo
claude
> /new-project
```

Option B: Copy template manually:
```bash
cp -r ad5-infrastructure/project-template/.claude your-new-repo/.claude
cp ad5-infrastructure/project-template/state.md your-new-repo/state.md
cp ad5-infrastructure/project-template/.gitignore your-new-repo/.gitignore
cp ad5-infrastructure/project-template/.gitattributes your-new-repo/.gitattributes
cp ad5-infrastructure/project-template/.env.example your-new-repo/.env.example
```

Then customize `.claude/CLAUDE.md` for that project's tech stack and requirements.

## Slash Commands

After installation, these are available in every Claude Code session:

| Command | What It Does |
|---------|-------------|
| `/new-project` | Scaffolds .claude/, state.md, .gitignore, .gitattributes into current repo |
| `/update-state` | Reads git log and file changes, updates state.md to match reality |
| `/phase-gate` | Runs build, standards, UI, and security checklist before phase completion |
| `/handoff` | Generates session summary so next session picks up cleanly |

## Updating Standards

When AD-5 standards evolve, update the files in this repo, then re-run the install commands. The canonical versions live here. Machine copies are just deployments.

## Key Decisions

- File names are NOT optional. Claude Code looks for `CLAUDE.md`, `.claude/settings.json`, `.claude/commands/*.md` specifically. Renaming breaks auto-loading.
- Global CLAUDE.md is concise bullet points, not prose. Anthropic recommends treating it like a prompt to be refined.
- Hooks are for deterministic enforcement (formatting, type checks, reminders). They fire regardless of what the model decides.
- Slash commands are for repeatable workflows. Natural language in .md files with `$ARGUMENTS` for parameters.
- CLAUDE.local.md is auto-gitignored. Use it for personal sandbox URLs, test data, machine-specific paths.

## References

- Claude Code Memory Docs: https://code.claude.com/docs/en/memory
- Claude Code Best Practices (Anthropic): https://www.anthropic.com/engineering/claude-code-best-practices
- Claude Code Settings: https://code.claude.com/docs/en/settings
