# CLAUDE.md Quick Start Guide

> Get your AI working like a professional developer in 5 minutes

---

## Step 1: Choose Your Template

### General Project
Copy `CLAUDE.md` to your project root:
```bash
cp templates/CLAUDE.md /path/to/your/project/CLAUDE.md
```

### Quantitative Trading Project
Copy `CLAUDE_QUANT.md`:
```bash
cp templates/CLAUDE_QUANT.md /path/to/your/project/CLAUDE.md
```

---

## Step 2: Customize Core Sections

Edit your CLAUDE.md and fill in:

### 1. Project Overview (3-5 lines)
```markdown
**Tech Stack**:
- Python 3.11
- FastAPI
- PostgreSQL

**Key Architecture**:
- REST API with layered architecture
- Repository pattern for data access
```

### 2. Commands (Add your actual commands)
```bash
# Build/Run
uvicorn app.main:app --reload

# Test
pytest tests/ -v

# Lint
ruff check .
```

### 3. Agent Docs (Create as needed)
```bash
mkdir -p agent_docs
cp templates/agent_docs/*.md /path/to/your/project/agent_docs/
```

---

## Step 3: Create Agent Docs (Optional but Recommended)

### Start with 2-3 docs:
1. `agent_docs/architecture.md` - Your system design
2. `agent_docs/code_conventions.md` - Your coding standards
3. `agent_docs/testing_guide.md` - Your testing approach

### Fill in with your actual project info:
- Add file:line references to real code
- Document your actual patterns
- Include real command examples

---

## Step 4: Verify Setup

Open Claude Code in your project and test:

```
You: "Help me understand the project structure"

AI should:
1. Read CLAUDE.md
2. Reference agent_docs/
3. Give project-specific guidance
```

---

## The Golden Rule

```
╔═══════════════════════════════════════════════════════╗
║  Never write code before completing Code Research.    ║
╚═══════════════════════════════════════════════════════╝
```

---

## Common Mistakes to Avoid

### ❌ Too Long
```markdown
# BAD: 500+ lines with every possible command
# Claude will ignore most of it
```

### ✅ Right Size
```markdown
# GOOD: 50-100 lines with pointers to detailed docs
```

### ❌ Generic Content
```markdown
# BAD: "Always write clean code"
# Claude already knows this
```

### ✅ Specific Instructions
```markdown
# GOOD: "Use Repository pattern, see agent_docs/architecture.md"
# Project-specific guidance
```

---

## File Structure Checklist

```
your-project/
├── CLAUDE.md                 # Main AI rules (< 100 lines)
├── agent_docs/
│   ├── architecture.md       # Your system design
│   ├── code_conventions.md   # Your coding standards
│   └── testing_guide.md      # Your testing approach
└── .claude/
    └── commands/             # Custom slash commands (optional)
```

---

## Next Steps

1. **Copy template** to your project
2. **Fill in** project-specific details
3. **Create agent_docs/** with real references
4. **Test** with a simple task
5. **Iterate** based on results

---

## Getting Help

- Read `docs/RESEARCH_REPORT.md` for deep understanding
- Check `templates/agent_docs/` for pattern examples
- Review `docs/DISCUSSION_SUMMARY.md` for design rationale
