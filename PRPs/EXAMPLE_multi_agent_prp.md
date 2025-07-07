# Example PRP: Multi-Agent System – Research Agent with Email Draft Sub-Agent

**Purpose**: Build a Pydantic AI multi-agent CLI application where a primary Research Agent uses Brave Search API and an Email Draft Agent (via Gmail API) as a tool.

**Core Principles**:

1. Context is King: Embed all documentation, code snippets, and gotchas.
2. Validation Loops: Include executable tests/lints for iterative fixes.
3. Information Dense: Use real file patterns from the codebase.
4. Progressive Success: Validate each stage before enhancing.

---

## Usage Commands

- **Generate this PRP**:

  ```bash
  gemini code --prompt "/generate-prp PRPs/EXAMPLE_multi_agent_prp_Gemini.md"
  ```

- **Execute this PRP**:

  ```bash
  gemini code --prompt "/execute-prp PRPs/EXAMPLE_multi_agent_prp_Gemini.md"
  ```

---

## 1. Goals & Scope

- **Goal**: Production-ready CLI app for research queries and email drafting.
- **Scope**:

  - Research Agent: queries Brave Search.
  - Email Agent: drafts Gmail emails.
  - Streamed, tool-aware CLI interaction.
  - Multi-LLM support & secure auth.

**Success Criteria**:

- Research Agent hits Brave API.
- Email Agent drafts via Gmail API.
- Agent-as-tool integration works.
- CLI streams results with tool metadata.
- 100% passing tests & style checks.

---

## 2. Context & References

### Documentation URLs

- [https://ai.pydantic.dev/agents/](https://ai.pydantic.dev/agents/) (agent creation)
- [https://ai.pydantic.dev/multi-agent-applications/](https://ai.pydantic.dev/multi-agent-applications/) (agent-as-tool)
- [https://developers.google.com/gmail/api/guides/sending](https://developers.google.com/gmail/api/guides/sending) (Gmail drafts)
- [https://api-dashboard.search.brave.com/app/documentation](https://api-dashboard.search.brave.com/app/documentation) (Brave API)

### Code Examples

- `examples/agent/agent.py` (agent registration)
- `examples/agent/providers.py` (LLM config)
- `examples/cli.py` (streaming CLI pattern)

---

## 3. Desired Structure

```
agents/
 ├ research_agent.py
 ├ email_agent.py
 ├ providers.py
 └ models.py

tools/
 ├ brave_search.py
 └ gmail_tool.py

config/settings.py
cli.py
.env.example
README.md
tests/
```

---

## 4. Known Gotchas

```markdown
- Pydantic AI: async-only functions in agents
- Gmail OAuth2: requires initial browser auth
- Brave API: rate-limited free tier
- Agent tools: must pass ctx.usage for cost tracking
- Gmail drafts: base64 + MIME formatting
- Store secrets in .env, never commit credentials
```

---

## 5. Implementation Blueprint

### Data Models (`agents/models.py`)

```python
from pydantic import BaseModel, Field
from typing import List, Optional

class ResearchQuery(BaseModel):
    query: str
    max_results: int = Field(10, ge=1, le=50)
    include_summary: bool = Field(True)

class BraveSearchResult(BaseModel):
    title: str
    url: str
    description: str
    score: float

class EmailDraft(BaseModel):
    to: List[str]
    subject: str
    body: str
    cc: Optional[List[str]] = None
    bcc: Optional[List[str]] = None
```

### Task List

1. **Setup Config**: `config/settings.py`, `.env.example`
2. **Brave Tool**: `tools/brave_search.py` (async httpx, Pydantic)
3. **Gmail Tool**: `tools/gmail_tool.py` (OAuth2, MIME)
4. **Email Agent**: `agents/email_agent.py` (@agent.tool, Pydantic)
5. **Research Agent**: `agents/research_agent.py` (multi-agent pattern)
6. **CLI**: `cli.py` (asyncio, streaming)
7. **Tests**: `/tests/*` (mock APIs, coverage ≥ 80%)
8. **Docs**: `README.md` (installs, usage, diagrams)

### Pseudocode Snippet

```python
# Task 2: Brave Tool
def setup_brave_tool(api_key: str):
    ...

# Task 5: Research Agent tool wrapper
def research_tool(ctx, query):
    results = await brave_search(query, ...)
    return results

@agent.tool
def create_email_draft(ctx, draft: EmailDraft):
    return await gmail_tool.create_draft(draft)
```

---

## 6. Validation Gates

```bash
# Style & Types
ruff check --fix && mypy .

# Unit Tests
pytest tests/ -v --cov
```

**Integration**:

```bash
python cli.py
# Simulate user queries and email drafting
```

---

## 7. Final Checklist

- [ ] Lint & type checks pass
- [ ] All unit/integration tests pass
- [ ] CLI flows work end-to-end
- [ ] README & .env.example updated
- [ ] No secrets in VCS

---

**Confidence**: 9/10 – comprehensive context, patterns, and validations ensure one-pass success.
