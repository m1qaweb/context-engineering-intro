# GEMINI.md

_Global rules and guidelines for every Gemini CLI session_

---

### 🔄 Project Awareness & Context

- **Always read `PLANNING.md`** at the start of a new session to understand architecture, goals, style, and constraints.
- **Check `TASK.md`** before beginning any work.

  - If your task isn’t listed, **add a new entry** with a concise title, description, and date.

- **Follow naming conventions, file structure, and architecture patterns** as defined in `PLANNING.md`.
- **Activate `venv_linux`** for all Python commands (including tests):

  ```bash
  source venv_linux/bin/activate
  ```

### 🧱 Code Structure & Modularity

- **Limit files to ≤ 500 lines**. If you hit the limit, refactor into modules or helpers.
- **Group code by feature/responsibility**. For agent projects, a common layout:

  ```
  ├── agent.py      # Main execution logic
  ├── tools.py      # Agent tool functions
  └── prompts.py    # System and user prompts
  ```

- **Prefer relative imports** within packages.
- **Manage secrets via [`python-dotenv`](https://github.com/theskumar/python-dotenv)**:

  ```python
  from dotenv import load_dotenv
  load_dotenv()
  ```

### 🧪 Testing & Reliability

- **Write Pytest unit tests** for every new function, class, or route.
- **After changing logic**, update any affected tests immediately.
- **Mirror your source layout** under `/tests`, e.g.:

  ```
  src/
  └── module/
      └── feature.py

  tests/
  └── module/
      └── test_feature.py
  ```

  Each test file should include:

  1. A normal “happy‑path” test
  2. At least one edge‑case test
  3. At least one failure/exception test

### ✅ Task Completion

- **After finishing a task**, mark it ✅ in `TASK.md`.
- **Log any new sub‑tasks** under a “Discovered During Work” section in `TASK.md`.

### 📎 Style & Conventions

- **Language**: Python
- **Formatting**: Follow PEP 8, use type hints, and run `black .` on every commit.
- **Data Validation**: Use [`pydantic`](https://pydantic-docs.helpmanual.io/).
- **Web Framework**: Use FastAPI; for the ORM prefer [`SQLModel`](https://sqlmodel.tiangolo.com/) or SQLAlchemy.
- **Docstrings**: Every function/class must have a Google‑style docstring, for example:

  ```python
  def fetch_user(user_id: int) -> User:
      """
      Retrieve a user by ID.

      Args:
          user_id (int): Unique identifier of the user.

      Returns:
          User: The user object corresponding to `user_id`.
      """
      ...
  ```

### 📚 Documentation & Explainability

- **Keep `README.md` up to date**: reflect new features, deps, and setup changes.
- **Comment any non‑obvious code**.
- For complex logic, add `# Reason:` comments explaining why something is implemented a certain way.

### 🧠 AI Behavior Rules

- **Never assume missing context**—ask clarifying questions if you’re unsure.
- **Only use verified libraries**; never hallucinate imports or functions.
- **Confirm file paths and module names exist** before referencing them.
- **Do not erase or overwrite existing code** unless a `TASK.md` entry explicitly directs you to do so.

---

_Save and commit `GEMINI.md`, then your Gemini‑CLI sessions will automatically pick up these rules._
