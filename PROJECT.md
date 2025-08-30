# Claude Multi-Agent System

## Overview
Shell-based system transforming Claude Code into four specialized AI assistants via dynamic personality switching.

## Tech Stack
- **Language**: Shell Script (Bash/Zsh)
- **Dependency**: Claude Code CLI
- **Platform**: macOS/Linux
- **Method**: File substitution (copying role.md → CLAUDE.md)

## The Agents

| Agent | Command | Role | Special Rule |
|-------|---------|------|--------------|
| **Selina** | `se`, `selina` | Analyst | Analyzes requirements |
| **Wayne** | `w`, `wayne` | Architect | Designs but never codes |
| **Shirley** | `s`, `shirley` | Coder | Implements perfectly |
| **Dylon** | `d`, `dylon` | Auditor | Reviews but never codes |

Continue sessions: `sec`, `wc`, `sc`, `dc`

## Core Mechanism
1. User types agent command (e.g., `w`)
2. System copies `~/.claude/architect.md` → `./CLAUDE.md`
3. Claude Code starts with Wayne's personality
4. On exit, `CLAUDE.md` is deleted

## File Structure
```
~/.claude/
├── analyst.md      # Selina
├── architect.md    # Wayne
├── coder.md       # Shirley
└── auditor.md     # Dylon

~/.functions       # Shell functions
~/.aliases         # Command aliases
```

## Key Functions
- `_run_claude_role()` - Core switching logic
- `claude-status` - System health check
- `claude-help` - Usage guide
- `claude-flow` - Full workflow automation

## Installation
1. Create `~/.claude/` directory
2. Copy role files to `~/.claude/`
3. Add functions to shell config
4. Source and enjoy

## The Joke
This entire system is unnecessary - Claude Code has `/agent` command built-in. But it works perfectly and was created BY Claude Code itself, achieving recursive meta-humor.

## Notes
- Each agent reads this PROJECT.md for context
- CLAUDE.md is temporary (auto-cleaned)
- Designed for individual developers
- No Windows support (POSIX shells only)