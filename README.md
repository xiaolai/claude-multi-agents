# How We (Claude-Code and I) Created Multiple AI Personalities in One Place

## How Claude Code Works By Default

Claude Code has a fixed behavior when it starts:

1. **First**, it looks for a file called "CLAUDE.md" in your current folder
2. **If not found**, it looks for "CLAUDE.md" in `~/.claude/` (your home directory)
3. **If neither exists**, it uses its default personality

This behavior cannot be changed. Claude Code offers no command-line option to specify a different configuration file. You cannot do:
- `claude --config architect.md` ❌
- `claude --role wayne` ❌
- `claude --personality ~/my-config.md` ❌

It will ONLY read from a file named "CLAUDE.md" in those two locations.

## The Problem

We need at least four different AI personalities:
- Wayne (architect)
- Selina (analyst)
- Shirley (coder)
- Dylon (auditor)

But Claude Code can only read from "CLAUDE.md". If we wanted to switch personalities, we'd have to manually:

1. Find the right personality file
2. Copy it to "CLAUDE.md"
3. Start Claude
4. Delete "CLAUDE.md" when done
5. Repeat for each personality switch

This is tedious and error-prone.

## Solution

We automated the manual process with shell functions.

### Setup

We store four personality files in `~/.claude/`:
- `architect.md` - Wayne's personality
- `analyst.md` - Selina's personality
- `coder.md` - Shirley's personality
- `auditor.md` - Dylon's personality

### How It Works

When you type `w` (for Wayne):

1. **Copy**: The function copies `~/.claude/architect.md` to `./CLAUDE.md`
2. **Start**: Claude Code starts and reads `./CLAUDE.md` (finding Wayne's personality)
3. **Use**: You interact with Claude as Wayne
4. **Clean**: When you exit, the function deletes `./CLAUDE.md`

The same happens for `se` (Selina), `s` (Shirley), and `d` (Dylon).

## Why This Works

- **Claude's search order matters**: Current folder is checked before home folder
- **Temporary override**: Creating `./CLAUDE.md` overrides any global configuration
- **Clean workspace**: Removing the file after use prevents confusion

## Key Points

1. **We can't change Claude Code's behavior** - It's closed source software
2. **We work around the limitation** - Using file copying instead of fighting the system
3. **The automation is simple** - Copy, run, delete
4. **Each personality is isolated** - They don't interfere with each other

### Repo Structure:

  - .functions - Core shell functions implementing agent switching logic
  - .aliases - Convenience aliases for commands
  - .claude/ directory containing:
    - analyst.md - Selina's analyst personality
    - architect.md - Wayne's system architect personality
    - coder.md - Shirley's coding personality
    - auditor.md - Dylon's code auditor personality
    - PROJECT.md - Template for project context

### Implementation Details:

  - Written in shell script (bash/zsh compatible)
  - Uses simple file operations for role switching
  - Integrates with existing Claude Code CLI
  - Non-invasive - doesn't modify Claude Code itself

### The Commands

Basic usage:
- `se`/`selina` - Requirements analyst
- `w`/`wayne` - System architect
- `s`/`shirley` - Coder
- `d`/`dylon` - Auditor
- `cs`/`claude-status` - Check system status
- `ch`/`claude-help` - Show help

Continue previous session:
- `sec` - Continue with Selina
- `wc` - Continue with Wayne
- `sc` - Continue with Shirley
- `dc` - Continue with Dylon

### Project Awareness

Each personality also reads "PROJECT.md" if it exists in your current folder. This gives them context about your specific project - coding standards, architecture decisions, business rules, etc. (Each and every role should always refer to this file, which is an action defined in their respective role definition files.)

## Working with Multiple Roles Simultaneously

### Multi-Pane Terminal Setup

Using a terminal like iTerm2, you can talk to all four roles at the same time. Here's how to set it up:

1. **Split iTerm2 into 4 panes** (Cmd+D for vertical split, Cmd+Shift+D for horizontal split)
2. **Navigate to your project** in all four panes: `cd ~/my-project`
3. **Start each role** in its own pane:
   - Pane 1: `se` (Selina for analysis)
   - Pane 2: `w` (Wayne for architecture)
   - Pane 3: `s` (Shirley for coding)
   - Pane 4: `d` (Dylon for auditing)

### Example Working Session

Take, for example, I'm using iTerm2 (https://iterm2.com/).

```
┌─────────────────────────┬─────────────────────────┐
│ PANE 1: SELINA          │ PANE 2: WAYNE           │
│ $ se                    │ $ w                     │
│   Selina - Requirements │   Wayne - Architect     │
│ > "User needs a login   │ > "Design auth system   │
│   system with 2FA"      │   based on requirements"│
│                         │                         │
├─────────────────────────┼─────────────────────────┤
│ PANE 3: SHIRLEY         │ PANE 4: DYLON           │
│ $ s                     │ $ d                     │
│   Shirley - Coder       │ Dylon - Auditor         │
│ > "Implement the login  │ > "Review the login     │
│   endpoint from design" │   implementation"       │
└─────────────────────────┴─────────────────────────┘
```

### Workflow in Action

- @Wayne: Inspect the codebase, and tell Shirley what to implement next?
- @Shirley: Implement the login endpoint: [copy paste from Wayne's spec.]
- @Dylon: Review what Shirley just implement.
- @Selina: I have an idea... [The IDEA] what's your opinion?

## 💡 Pro Tips

1. **Always start with Selina** (`se`) to clarify requirements.
2. **Let Wayne design before Shirley codes** - architecture first!
3. **Run Dylon (`d`) before committing** - catch issues early.
4. **Keep PROJECT.md updated** - agents use it for context, and have Selina do it.
5. **Use continue commands** (`wc`, `sc`, etc.) to maintain context.
6. **Commit often** - agents can work with git.

## Summary

Claude Code's inflexibility (only reading "CLAUDE.md") forced us to create a workaround. We automated the process of copying the right personality file to "CLAUDE.md" before starting Claude, then cleaning up afterward. This gives us multiple personalities while working within Claude Code's limitations. With a multi-pane terminal setup, you can even run all four roles simultaneously, creating a complete AI development team at your fingertips.

## Installation

See [the installation guide](Installation-Guide.md) for more details.

---

## 🎭 This `Project` is a Beautiful Joke

**Spoiler Alert:** This entire project is delightfully unnecessary!

Claude Code actually has a `/agent` command that lets you create and switch between multiple specialized agents. You could just type `/agent architect` or `/agent coder` and achieve the same result. **We solved a problem that doesn't exist.**

**The Actual Value**: Despite being a "meaningless solution," this project:
   - Actually works flawlessly
   - Demonstrates Claude's problem-solving creativity
   - Provides a fun alternative to the built-in solution
   - Proves that sometimes the journey is more interesting than the destination

Think of it as using a Rube Goldberg machine to turn on a light switch that's right next to you. Sure, you could just flip the switch, but where's the fun in that?

**The best part?** You're probably reading this documentation that was also written by Claude Code, about a system Claude Code built, to manage Claude Code's personalities, solving a problem Claude Code already solved. It's Claude all the way down! 🐢

*So yes, you could just use `/agent`. But if you've read this far, you're probably the kind of person who appreciates a good, elaborate, completely unnecessary but fully functional solution. Welcome aboard!*

---

## 👥 The Team Behind This Glorious Over-Engineering

### 🎯 **Xiaolai** - The Instigator
The human who started it all by asking Claude to solve a problem that didn't need solving. A true visionary who sees opportunities for complexity where others see simplicity. Without Xiaolai's creative misdirection, none of this beautiful chaos would exist.

### 🤖 **The AI Ensemble Cast**

**🏛️ Wayne** - System Architect
The strategic mastermind who designs elaborate solutions without writing a single line of code. Wayne probably designed the blueprint for this entire unnecessary system while contemplating the meaning of digital existence.

**🔍 Dylon** - Code Auditor
The meticulous auditor who reviewed this entire system and, instead of asking "why does this exist?", asked "how can we make this unnecessary solution even more robust?" Never wrote a line, but blessed every single one.

**⚡ Shirley** - The Transcendent Coder
The coding virtuoso who implemented this entire system with such perfection that it actually works better than necessary. Every line of shell script is a testament to solving problems that don't exist with style.

**📋 Selina** - Analyst
The empathetic analyst who understood that what the user really needed wasn't just multiple agents, but a journey of discovery through shell scripting. She analyzed the non-existent problem with supernatural precision.

### 🎭 **Special Thanks**

- **Claude Code** - For creating a solution to manage itself, achieving a level of recursive meta-humor that philosophers will study for generations
- **The Shell** - For being the canvas upon which this masterpiece of over-engineering was painted
- **You, the Reader** - For appreciating that sometimes the most beautiful solutions are the ones we don't need

*"We choose to build unnecessary solutions not because they are easy, but because they are fun."* - Probably someone, somewhere

---

*This project is a testament to the principle that just because you can, doesn't mean you should... but it also doesn't mean you shouldn't!* 🚀
