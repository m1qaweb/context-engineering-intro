# Context Engineering Template for Gemini CLI

A comprehensive template for getting started with Context Engineering—the discipline of engineering context for AI coding assistants so they have the information necessary to get the job done end to end.

> **Context Engineering is 10× better than prompt engineering and 100× better than vibe coding.**

## 🚀 Quick Start

````bash
# 1. Clone this template
```bash
git clone https://github.com/coleam00/Context-Engineering-Intro.git
cd Context-Engineering-Intro
````

```bash
# 2. Set up your project rules (optional)
# Edit GEMINI.md to add your project-specific guidelines
```

```bash
# 3. Add examples (highly recommended)
# Place relevant code examples in the examples/ folder
```

```bash
# 4. Create your initial feature request
# Edit INITIAL.md with your feature requirements
```

```bash
# 5. Generate a comprehensive PRP (Product Requirements Prompt)
gemini code --prompt "/generate-prp INITIAL.md"
```

```bash
# 6. Execute the PRP to implement your feature
gemini code --prompt "/execute-prp PRPs/your-feature-name.md"
```

---

## 📚 Table of Contents

- [What is Context Engineering?](#what-is-context-engineering)
- [Template Structure](#template-structure)
- [Step-by-Step Guide](#step-by-step-guide)
- [Writing Effective INITIAL.md Files](#writing-effective-initialmd-files)
- [The PRP Workflow](#the-prp-workflow)
- [Using Examples Effectively](#using-examples-effectively)
- [Best Practices](#best-practices)
- [Resources](#resources)

---

## What is Context Engineering?

A paradigm shift from prompt engineering:

### Prompt Engineering vs Context Engineering

| Prompt Engineering                     | Context Engineering                                       |
| -------------------------------------- | --------------------------------------------------------- |
| Focuses on clever wording and phrasing | A complete system providing comprehensive project context |
| Like giving someone a sticky note      | Like writing a full screenplay with all the details       |

### Why It Matters

1. **Reduces AI Failures**: Most agent errors stem from missing context, not model limitations.
2. **Ensures Consistency**: AI follows your project’s patterns, style, and conventions.
3. **Enables Complex Features**: Multi-step implementations succeed with full context.
4. **Self-Correcting**: Validation loops let the AI detect and fix its own mistakes.

---

## Template Structure

```bash
tree -L 2
```

```
context-engineering-intro/
├── .gemini/
│   ├── commands/
│   │   ├── generate-prp.md    # Generates comprehensive PRPs
│   │   └── execute-prp.md     # Executes PRPs to implement features
│   └── settings.local.json    # Gemini CLI settings
├── PRPs/
│   ├── templates/
│   │   └── prp_base.md       # Base template for PRPs
│   └── EXAMPLE_multi_agent_prp_Gemini.md  # Example of a complete PRP
├── examples/                  # Your code examples (critical!)
├── GEMINI.md                  # Global rules for AI assistant
├── INITIAL.md                 # Template for feature requests
├── INITIAL_EXAMPLE.md         # Example feature request
└── README.md                  # This file
```

> **Note**: This template focuses on context engineering itself; RAG and external tools will be covered in future releases.

---

## Step-by-Step Guide

### 1. Set Up Global Rules (`GEMINI.md`)

The `GEMINI.md` file contains project-wide rules that the AI assistant will follow in every Gemini CLI session. Use the provided template or customize it for your project:

- **Project Awareness**: How to read planning docs and locate tasks.
- **Code Structure**: File size limits, module organization.
- **Testing Requirements**: Unit test patterns and coverage expectations.
- **Style Conventions**: Language preferences and formatting rules.
- **Documentation Standards**: Docstring formats and commenting guidelines.

---

### 2. Create Your Initial Feature Request (`INITIAL.md`)

Use this template:

```markdown
## FEATURE:

Describe the functionality you want, including detailed requirements.

## EXAMPLES:

List example files in `examples/` and how to use them.

## DOCUMENTATION:

Link to relevant API docs, architecture diagrams, or schemas.

## OTHER CONSIDERATIONS:

Authentication, rate limits, performance constraints, etc.
```

Refer to `INITIAL_EXAMPLE.md` for a filled-out example.

---

### 3. Generate the PRP

Run:

```bash
gemini code --prompt "/generate-prp INITIAL.md"
```

This will:

1. Read your feature request.
2. Analyze the codebase for patterns.
3. Gather relevant documentation and examples.
4. Produce `PRPs/your-feature-name.md` with context, implementation blueprint, and validation gates.

---

### 4. Execute the PRP

Run:

```bash
gemini code --prompt "/execute-prp PRPs/your-feature-name.md"
```

The assistant will:

1. Load the PRP context.
2. Plan tasks via `TodoWrite`.
3. Implement code and tests incrementally.
4. Run validations (lint, type, unit tests).
5. Iterate until all gates pass.

---

## Writing Effective `INITIAL.md` Files

- **FEATURE**: Be explicit and detailed.
- **EXAMPLES**: Show patterns; include both correct and incorrect usage.
- **DOCUMENTATION**: Include URLs to all relevant resources.
- **OTHER CONSIDERATIONS**: Note auth flows, quotas, and edge cases.

---

## The PRP Workflow

### How `/generate-prp` Works

1. **Research**: Codebase patterns, external docs, best practices.
2. **Assemble Context**: Combine internal and external references.
3. **Blueprint**: Draft pseudocode, task list, and error handling.
4. **Validation Gates**: Add lint and test commands.
5. **Quality Check**: Score confidence and completeness.

### How `/execute-prp` Works

1. **Load Context**: Reads PRP file.
2. **Plan**: Generates task list with `TodoWrite`.
3. **Implement**: Writes code and tests.
4. **Validate**: Runs gates and fixes failures.
5. **Complete**: Marks tasks done and prepares a draft PR.

---

## Using Examples Effectively

Examples in `examples/` are critical:

- **Code Structure Patterns**: Module organization and imports.
- **Testing Patterns**: Unit, integration, and mocking.
- **Integration Examples**: API clients and DB connections.
- **CLI Patterns**: Streaming, argument parsing, and error handling.

---

## Best Practices

1. **Be Explicit**: Don’t assume unstated preferences.
2. **Comprehensive Examples**: More examples = better results.
3. **Validation Gates**: Ensure working code on the first pass.
4. **Leverage Documentation**: Link to official and internal docs.
5. **Customize `GEMINI.md`**: Tailor rules for your project.

---

## Resources

- [Gemini CLI Docs](https://developers.google.com/ai/gemini/cli)
- [Context Engineering Best Practices](https://www.philschmid.de/context-engineering)

---

_Happy Context Engineering with Gemini CLI!_
