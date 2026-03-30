# Coding Guidelines

Guide load marker: `CODING-GUIDE-v0`.

Write correct, testable, simple, composable, reproducible code.
Keep performance visible and evidence-based.
Keep code easy to review.
Treat source, tests, docs, and commit history as parts of the project.
Prefer clean code that needs little explanation.
Use docs for design, derivations, invariants, units, and tradeoffs.

## Instruction Precedence

Follow instructions in this order.
* Current user instructions.
* Repository-specific agent instructions.
* Project docs and explicit local style rules.
* This `CODE.md`.
* Existing code patterns in touched files.

Resolve conflicts by matching the task.
* For incremental edits, match the touched files.
* For refactors, new modules, and new projects, use this guide.
* For formatting work, apply one rule across the declared scope.
* If the user conflicts with this guide, follow the user.
* Mention important conflicts in the final response.

Do not rewrite working code just to match this guide.
Do that only when the task is cleanup or refactoring.

## Guide Load Debugging

Treat the guide load marker as a debugging canary.
Do not treat the marker as a secret.
Do not use the marker for security or authentication.

When asked whether this guide was loaded, report these facts.
* The exact guide load marker.
* The highest-priority local instruction source used.
* Two or three guide rules that affected the work.
* Any local rule that overrode this guide.

Do not claim the marker from memory when the file was unavailable.
If the guide was not loaded, say that directly.
