# Base PRP Template v2 – Gemini CLI Edition

**A context-rich scaffold with validation loops for AI-driven feature implementation**

---

## Purpose

Template optimized for Gemini CLI agents to implement features with comprehensive context and self-validation capabilities, ensuring working code via iterative refinement.

## Core Principles

1. **Context is King**: Embed all necessary documentation, examples, and caveats.
2. **Validation Loops**: Provide executable tests and lint commands for self-correction.
3. **Information Dense**: Reference real files, patterns, and keywords from the codebase.
4. **Progressive Success**: Build incrementally—validate simple steps before adding complexity.
5. **Global Rules**: Follow all guidelines in `GEMINI.md`.

---

## 1. Goal

> _What needs to be built?_
> Describe the desired end state, including user-visible behavior and technical specifications.

## 2. Why

- **Business Value**: Explain impact and who benefits.
- **Integration**: How it fits with existing features.
- **Problems Solved**: Outline pain points addressed.

## 3. What

Detail user interactions and system requirements:

- CLI commands or API endpoints
- Data flows and state changes
- Performance or security constraints

### Success Criteria

- [ ] List specific, measurable outcomes (e.g., tests, performance metrics).

---

## 4. All Needed Context

Provide every piece of context the AI needs:

### Documentation & References

```yaml
# MUST INCLUDE
- url: [Official API docs URL]
  why: [Sections/methods required]

- file: [path/to/example.py]
  why: [Pattern to follow]

- doc: [Library docs URL]
  section: [Key section]
  critical: [Gotcha to avoid]

- docfile: [local/path/to/doc.md]
  why: [User-provided project docs]
```

### Current Codebase Snapshot

```bash
# Run in project root:
tree -L 2
```

_(Paste relevant output here.)_

### Desired Codebase Changes

```bash
# Outline new files and their responsibilities:
# e.g.,
#   src/feature_x.py – core logic
#   tests/test_feature_x.py – unit tests
```

### Known Gotchas & Library Quirks

```python
# CRITICAL: [Library] requires [setup]
# e.g., FastAPI endpoints must be async
# e.g., Pydantic v2 model creation differs from v1
```

---

## 5. Implementation Blueprint

### Data Models & Structure

```python
# Examples:
#   - ORM models
#   - Pydantic schemas
#   - Validators
```

Define key data structures with types and constraints.

### Task List (YAML)

```yaml
Task 1:
  MODIFY src/existing_module.py:
    FIND: "class OldImplementation"
    INJECT after: "def __init__"
    NOTES: Preserve existing method signatures

Task 2:
  CREATE src/new_feature.py:
    TEMPLATE_FROM: src/similar_feature.py
    MODIFY: class name and core logic
    PATTERN: Error handling matches existing patterns
```

### Task Pseudocode

```python
# Task 2 Pseudocode
async def new_feature(param: str) -> Result:
    # PATTERN: Input validation via src/validators.py
    validated = validate_input(param)

    # GOTCHA: External API rate limits – use retry decorator
    @retry(attempts=3)
    async def call_api():
        return await external_api.fetch(validated)

    data = await call_api()
    return format_response(data)
```

### Integration Points

```yaml
DATABASE:
  migration: "Add column 'feature_enabled' to users"
  index: "CREATE INDEX idx_feature ON users(feature_id)"

CONFIG:
  file: config/settings.py
  pattern: "FEATURE_TIMEOUT = int(os.getenv('FEATURE_TIMEOUT', '30'))"

ROUTES:
  file: src/api/routes.py
  pattern: "router.include_router(feature_router, prefix='/feature')"
```

---

## 6. Validation Loop

### Level 1: Syntax & Style

```bash
ruff check . --fix
mypy .
```

_Expect zero errors before proceeding._

### Level 2: Unit Tests

```bash
pytest tests/ -v
```

_Iterate: fix failures, re-run until all pass._

### Level 3: Integration Test

```bash
# Start service:
python -m src.main --dev

# Test via CLI or HTTP:
curl -X POST http://localhost:8000/feature -d '{"param":"value"}'
```

_Verify expected output and logs._

---

## 7. Final Validation Checklist

- [ ] All lints and type checks pass.
- [ ] All unit/integration tests pass.
- [ ] Manual end-to-end test succeeds.
- [ ] Documentation (README, examples) updated.
- [ ] No sensitive info committed.

---

## 8. Anti-Patterns to Avoid

- ❌ Don’t reinvent existing patterns.
- ❌ Don’t skip validation steps.
- ❌ Don’t use sync code in async contexts.
- ❌ Don’t hardcode secrets or magic numbers.
- ❌ Don’t catch broad exceptions.

---

_Save this file as `PRPs/templates/prp_base.md`. Use it as the foundation for all feature PRPs generated via Gemini CLI._
