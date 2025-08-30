# Claude Multi-Agent System - Installation Guide

A powerful system that transforms Claude Code into a team of specialized AI assistants for software development.

## 🎯 What This Does

Instead of using Claude Code as a single generalist AI, this system gives you four specialized experts:

- **Selina** (`se`) - Analyst who understands user needs
- **Wayne** (`w`) - System Architect who designs but never codes
- **Shirley** (`s`) - Perfect Coder who implements solutions
- **Dylon** (`d`) - Code Auditor who reviews but never codes

## 📋 Prerequisites

Before installing, ensure you have:

1. **Claude Code installed** and working
   ```bash
   # Test if Claude Code is installed
   claude --version
   ```
   If not installed, visit [Claude Code documentation](https://docs.anthropic.com/claude-code)

2. **macOS/Linux with zsh or bash**
   ```bash
   # Check your shell
   echo $SHELL
   ```

3. **Home directory with write permissions**
   ```bash
   # You should be able to create folders here
   ls -la ~/
   ```

## 🚀 Installation Steps

### Step 1: Create the Claude Configuration Directory

```bash
# Create the .claude directory in your home folder
mkdir -p ~/.claude

# Verify it was created
ls -la ~/.claude
```

### Step 2: Download and Install Role Definition Files

Save each of these files to `~/.claude/`:

```bash
# Navigate to the claude directory
cd ~/.claude

# Create architect.md
cat > architect.md << 'EOF'
[Copy content from architect.md in the artifact]
EOF

# Create analyst.md
cat > analyst.md << 'EOF'
[Copy content from analyst.md in the artifact]
EOF

# Create coder.md
cat > coder.md << 'EOF'
[Copy content from coder.md in the artifact]
EOF

# Create auditor.md
cat > auditor.md << 'EOF'
[Copy content from auditor.md in the artifact]
EOF
```

**Alternative: Manual Creation**
1. Open your text editor
2. Create four new files in `~/.claude/`
3. Copy the content from the artifact for each role
4. Save as: `architect.md`, `analyst.md`, `coder.md`, `auditor.md`

### Step 3: Set Up Shell Functions

The setup depends on your shell configuration style:

#### Option A: If you use separate .functions file (Recommended)

```bash
# Check if you have a .functions file
ls -la ~/.functions

# If it doesn't exist, create it
touch ~/.functions

# Add the Claude functions to your .functions file
cat >> ~/.functions << 'EOF'

[Copy the entire functions.sh content from the artifact]
EOF
```

#### Option B: If you prefer everything in `.zshrc`/`.bashrc`

```bash
# For zsh users
cat >> ~/.zshrc << 'EOF'

[Copy the entire functions.sh content from the artifact]
EOF

# For bash users
cat >> ~/.bashrc << 'EOF'

[Copy the entire functions.sh content from the artifact]
EOF
```

### Step 4: Set Up Aliases

```bash
# Check if you have an .alias file
ls -la ~/.alias

# If it doesn't exist, create it
touch ~/.alias

# Add the Claude aliases
cat >> ~/.alias << 'EOF'

# ===== Claude Multi-Agent Aliases =====
# Utility shortcuts
alias cs='claude-status'
alias ch='claude-help'
alias cf='claude-flow'
alias ci='claude-init-project'
alias cl='claude-last'
EOF
```

### Step 5: Configure Shell to Load Functions and Aliases

This is crucial - your shell needs to load these files on startup.

#### For Zsh Users (.zshrc)

```bash
# Edit your .zshrc
nano ~/.zshrc

# Add these lines if they don't exist:
# Load functions
[ -f ~/.functions ] && source ~/.functions

# Load aliases
[ -f ~/.alias ] && source ~/.alias

# Save and exit (Ctrl+X, then Y, then Enter)
```

#### For Bash Users (.bashrc)

```bash
# Edit your .bashrc
nano ~/.bashrc

# Add these lines if they don't exist:
# Load functions
if [ -f ~/.functions ]; then
    source ~/.functions
fi

# Load aliases
if [ -f ~/.alias ]; then
    source ~/.alias
fi

# Save and exit (Ctrl+X, then Y, then Enter)
```

#### For macOS Users - Important Note!

macOS Terminal app doesn't read `.bashrc` by default. You need to also update `.bash_profile`:

```bash
# For bash on macOS
echo 'source ~/.bashrc' >> ~/.bash_profile
```

### Step 6: Reload Your Shell Configuration

```bash
# For zsh
source ~/.zshrc

# For bash
source ~/.bashrc

# Or simply close and reopen your terminal
```

### Step 7: Verify Installation

```bash
# Check if the system is installed correctly
claude-status

# You should see:
# ✅ Wayne (Architect) - wayne, w, wc
# ✅ Selina (Requirements) - selina, se, sec
# ✅ Shirley (Coder) - shirley, s, sc
# ✅ Dylon (Auditor) - dylon, d, dc

# Test a command
w --help
# Should show: 🏛️ Wayne - Legendary System Architect
# Then Claude Code help information
```

## 🎮 Basic Usage

### Quick Start Commands

```bash
# Start an analysis session with Selina
se

# Start an architecture session with Wayne
w

# Start a coding session with Shirley
s

# Start an audit session with Dylon
d

# Continue previous sessions
sec  # Continue with Selina
wc   # Continue with Wayne
sc   # Continue with Shirley
dc   # Continue with Dylon

# Check system status
cs

# Get help
ch
```

### Your First Workflow

```bash
# 1. Navigate to your project
cd ~/my-project

# 2. Create a PROJECT.md (optional but recommended)
cat > PROJECT.md << 'EOF'
# Project: My Awesome App

## Technology Stack
- Language: Python
- Framework: FastAPI
- Database: PostgreSQL

## Coding Standards
- Style Guide: PEP 8
- Testing: Pytest with 80% coverage
EOF

# 3. Start with requirements
se
> "I need a user authentication system"

# 4. Design the architecture
w
> "Design the auth system based on Selina's requirements"

# 5. Implement the code
s
> "Implement the login endpoint from Wayne's design"

# 6. Audit the implementation
d
> "Review the authentication implementation"

# 7. Fix any issues
sc
> "Address Dylon's security concerns"
```

## 🔧 Troubleshooting

### Issue: "command not found: w" (or any agent command)

**Solution 1:** Functions not loaded
```bash
# Check if functions are loaded
type _run_claude_role

# If "not found", reload your shell config
source ~/.zshrc  # or ~/.bashrc
```

**Solution 2:** Path to functions file incorrect
```bash
# Verify the file exists
ls -la ~/.functions

# Check if it's being sourced
grep "functions" ~/.zshrc  # or ~/.bashrc
```

### Issue: "claude: command not found"

Claude Code is not installed or not in PATH:
```bash
# Check if claude is installed
which claude

# If not found, install Claude Code first
npm install -g @anthropic-ai/claude-code
```

### Issue: Role files not found

```bash
# Check if files exist
ls -la ~/.claude/

# Should show:
# architect.md
# auditor.md
# coder.md
# requirements.md

# If missing, go back to Step 2
```

### Issue: Changes not taking effect

```bash
# Force reload everything
exec $SHELL

# Or completely restart terminal
exit
# Then open a new terminal
```

### Issue: Aliases not working

```bash
# Check if aliases are loaded
alias | grep claude

# If not shown, check your alias file
cat ~/.alias

# Ensure it's sourced in your shell config
grep "alias" ~/.zshrc  # or ~/.bashrc
```

## 📁 Project Templates

### Creating a New Project with Context

```bash
# Use the built-in project initializer
claude-init-project my-new-app

# This creates:
# - Project directory
# - Git repository
# - PROJECT.md template
# - Starts analysis with Selina
```

### PROJECT.md Template

Every project can have a `PROJECT.md` file that all agents will read:

```markdown
# Project: [Your Project Name]

## Overview
Brief description of what this project does

## Technology Stack
- Language: TypeScript
- Framework: Next.js
- Database: PostgreSQL
- Testing: Jest

## Coding Standards
- Style Guide: Airbnb
- Commit Format: Conventional Commits

## Architecture Decisions
- Pattern: Clean Architecture
- API Style: REST

[... see full template in artifact ...]
```

## 📚 File Structure Reference

After installation, you'll have:

```
~/
├── .claude/
│   ├── architect.md      # Wayne's personality
│   ├── requirements.md   # Selina's personality
│   ├── coder.md         # Shirley's personality
│   └── auditor.md       # Dylon's personality
├── .functions           # Shell functions (or in .zshrc/.bashrc)
├── .alias              # Aliases (or in .zshrc/.bashrc)
└── .zshrc or .bashrc   # Shell configuration

Your projects:
~/my-project/
├── PROJECT.md          # Project context (optional)
├── src/               # Your code
└── [NO CLAUDE.md]     # Cleaned up automatically!
```

## 🎉 You're Ready!

Try your first command:
```bash
w
# You should see: 🏛️ Wayne - Legendary System Architect
# Then Claude will start in architect mode!
```

Welcome to your new AI development team! Each specialist is now just two keystrokes away.

## 💡 Pro Tips

1. **Always start with Selina** (`se`) to clarify requirements
2. **Let Wayne design before Shirley codes** - architecture first!
3. **Run Dylon (`d`) before committing** - catch issues early
4. **Keep PROJECT.md updated** - agents use it for context
5. **Use continue commands** (`wc`, `sc`, etc.) to maintain context
6. **Commit often** - agents can work with git

## 🤝 Contributing

Found a bug or have an improvement? The system is just shell functions - feel free to customize!

---

*Remember: These aren't just different prompts - they're different specialists. Treat them as your personal development team!*
