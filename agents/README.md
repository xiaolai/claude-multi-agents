# Claude Code Agent Definitions

These are specialized agent personalities for Claude Code, designed to work with the built-in `/agent` command.

## Installation

### Option 1: Copy to Claude's agents directory
```bash
# Copy all agents to Claude's default location
cp *.md ~/.claude/agents/
```

### Option 2: Use directly with /agent command
```bash
# In Claude Code, load an agent:
/agent selina-analyst
/agent wayne-architect
/agent shirley-coder
/agent dylon-auditor
```

## The Agents

### 📋 Selina - The Analyst
**File**: `selina.md`  
**Command**: `/agent selina`  
**Role**: Master analyst who transforms data into strategic insights  
**Special**: Focuses on requirements analysis and pattern recognition  
**Tools**: Read, Write, Edit, Bash, Grep, Glob, WebSearch, WebFetch, TodoWrite

### 🏛️ Wayne - The Architect
**File**: `wayne.md`  
**Command**: `/agent wayne`  
**Role**: System architect who designs but never codes  
**Special**: Creates blueprints and implementation instructions  
**Tools**: Read, Grep, Glob, WebSearch, WebFetch, TodoWrite

### ⚡ Shirley - The Coder
**File**: `shirley.md`  
**Command**: `/agent shirley`  
**Role**: Transcendent coder who implements perfect solutions  
**Special**: Writes flawless code and teaches through implementation  
**Tools**: Read, Write, Edit, MultiEdit, NotebookEdit, Bash, Grep, Glob, WebSearch, WebFetch, TodoWrite, Task

### 🔍 Dylon - The Auditor
**File**: `dylon.md`  
**Command**: `/agent dylon`  
**Role**: Supreme code auditor who reviews but never codes  
**Special**: Finds vulnerabilities and ensures code quality  
**Tools**: Read, Grep, Glob, WebSearch, WebFetch, TodoWrite

## Workflow Example

```bash
# 1. Start with analysis
/agent selina
> "Analyze the requirements for a user authentication system"

# 2. Design the architecture
/agent wayne
> "Design the authentication system based on the requirements"

# 3. Implement the solution
/agent shirley
> "Implement the login endpoint from Wayne's design"

# 4. Audit the implementation
/agent dylon
> "Review the authentication implementation for security issues"
```

## Agent Personalities

Each agent has a distinct personality and approach:

- **Selina**: Empathetic, thorough, finds patterns others miss
- **Wayne**: Strategic, abstract thinker, never touches code
- **Shirley**: Confident, perfectionist, teaches while coding
- **Dylon**: Meticulous, security-focused, never writes code

## Key Rules

1. **Wayne and Dylon never write code** - They design and review only
2. **All agents respond in English only** - Regardless of input language
3. **Each agent has specialized tools** - Optimized for their role
4. **Agents can reference each other's work** - For seamless workflow

## The Meta-Joke

These agents recreate the shell-script system that was built to solve a problem that didn't exist (since `/agent` already exists). But now they work *with* the `/agent` command, making the joke even more recursive. It's Claude agents all the way down! 🐢