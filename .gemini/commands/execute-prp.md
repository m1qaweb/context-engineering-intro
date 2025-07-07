# /execute-prp Command Definition for Gemini CLI

This command reads and executes a Product Requirements Prompt (PRP) file end-to-end, following all context and validation steps.

## Usage

```bash
# Execute a PRP file:
gemini code --prompt "/execute-prp PRPs/your-feature-name.md"
```

## Workflow

1. **Load PRP File**

   - Read the specified PRP markdown to gather all context, requirements, and validation instructions.
   - Confirm availability of code examples, documentation links, and project rules (e.g., `GEMINI.md`).
   - If context is missing, prompt user for details or perform web research.

2. **Planning (ULTRATHINK)**

   - Deeply analyze the PRP goals.
   - Break down the feature into granular tasks using `TodoWrite`.
   - Identify and reuse existing code patterns for consistency.

3. **Implementation**

   - Sequentially execute tasks from the Todo list:

     - Generate or modify source files.
     - Add or update unit tests in `/tests`.
     - Ensure each change adheres to global rules in `GEMINI.md`.

4. **Validation**

   - Run validation commands defined in PRP (e.g., `pytest`, `flake8`).
   - Report pass/fail for each gate.
   - On failure, use error-handling patterns from the PRP to fix issues and re-run validations.

5. **Completion**

   - Summarize completed tasks.
   - Update `TASK.md`: mark tasks done and add any discovered sub-tasks.
   - Optionally, open a diff or draft pull request for review.

6. **Repeat & Resume**

   - You can re-run or resume execution at any point:

   ```bash
   gemini code --prompt "/execute-prp PRPs/your-feature-name.md"
   ```
