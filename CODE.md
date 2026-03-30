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

## Terminology

Use these terms consistently.
* Verification asks whether we built it right.
  Evidence shows requirements are met.
* Validation asks whether we built the right thing.
  Evidence shows intended use is satisfied in the intended environment.
* Input validation checks external input at a boundary.
  It is not product validation.
* Checks collect evidence for verification or validation.
  Examples include tests, builds, lint, benchmarks, and diff review.
* Tests are executable checks.

Do not use validation to mean tests, review, or general verification.

## Universal Principles

### Plan Before Coding

Think before coding on every nontrivial task.
Do not assume.
Do not hide confusion.
Surface tradeoffs before implementation.

* Read nearby code before changing behavior.
* Read relevant tests before changing behavior.
* Read relevant docs before changing public behavior.
* State important assumptions explicitly.
* Present plausible interpretations instead of choosing silently.
* Push back when a simpler approach satisfies the request.
* Name confusion directly when important facts are unclear.
* Ask when ambiguity affects correctness, API, safety, or data loss.
* Ask when ambiguity affects performance, compatibility, or history.
* Use judgment for typo fixes and obvious one-line changes.

Planning is not ceremony.
Planning is the minimum reasoning needed to avoid wrong assumptions.

### Correctness First

Make correctness the first design constraint.

* Preserve data meaning, units, APIs, schemas, and formats.
* Preserve user-visible behavior.
* Treat signs and coordinate conventions as contracts.
* Treat precision, layout, and tolerances as contracts.
* Perform input validation at boundaries.
* Use assertions for internal invariants.
* Do not hide behavior changes inside easier implementations.
* Fix bugs without creating new user-visible problems.

For scientific or data-heavy code, protect these properties.

* Units and dimensions.
* Numerical stability.
* Error bounds and tolerances.
* Reproducibility.
* Backend differences.
* Precision and layout.
* Known identities, invariants, and reference values.

### Verification By Design

Design code so correctness can be checked cheaply and repeatedly.
Use pragmatic test-driven development for specified behavior.
Use tests to protect behavior, not implementation trivia.

* Write tests first for bug fixes when practical.
* Write tests first for input validation behavior.
* Write tests first for specified public behavior.
* Use judgment for mechanical edits and exploratory design.
* Put pure behavior in directly testable functions.
* Keep I/O, plotting, logging, and networking at boundaries.
* Keep command-line parsing at boundaries.
* Expose real examples for user workflows.
* Add regression tests for bug fixes.
* Add reference tests for scientific code.
* Add end-to-end tests for important workflows.
* Make performance claims testable.
* Build test seams into architecture.
* Build input validation paths into architecture.

Simplify code that cannot be tested.
Split code that cannot be tested.
Give hard-to-test code a narrower interface.

### Simplicity First

Write the smallest design that solves the real problem.
Clean code makes ordinary behavior obvious.

* Do not add unrequested features.
* Do not add unused configuration knobs.
* Do not add speculative abstraction.
* Do not add unrequested flexibility.
* Do not add elaborate handling for impossible internal states.
* Always validate external input at boundaries.
* Add complexity only for current requirements.
* Remove complexity that does not pay for itself.
* Prefer direct code over clever code.

Simplicity does not mean avoiding architecture.
Every abstraction needs a clear job.
Every abstraction needs a clear reason to exist.
Simplify any solution that is much larger than the problem.

### Make State Explicit

Make important state visible.

* Make ownership explicit.
* Make units explicit.
* Make shape, precision, and layout explicit.
* Make configuration defaults explicit.
* Make cache keys explicit.
* Make cache invalidation rules explicit.
* Make lifecycle and cleanup paths explicit.
* Make concurrency and locking assumptions explicit.

Avoid hidden mutable state unless the framework requires it.
Avoid hidden mutable state unless performance requires it.
Document necessary hidden state.
Document who owns hidden state.
Document when hidden state changes.

### Composability

Design reusable code to compose with the surrounding system.

* Keep pure computation separate from I/O.
* Keep pure computation separate from networking.
* Keep pure computation separate from logging and plotting.
* Keep pure computation separate from command-line parsing.
* Keep data conversion at boundaries.
* Keep the hot path small and explicit.
* Keep APIs usable in scripts, tests, notebooks, and services.
* Keep APIs usable in batch jobs and larger workflows.
* Design functions to be callable independently when practical.

### Reproducibility

Make the project rebuildable, testable, and understandable later.

* Keep generated artifacts out of source unless tracked deliberately.
* Document how to regenerate generated files.
* Pin or bound dependencies where reproducibility matters.
* Seed random number generators to known values for reproducibility.
* Keep release steps documented.
* Keep examples and tests aligned with public behavior.
* Do not make notebooks the only source of truth.
* Do not make manual commands the only source of truth.

### Performance With Evidence

Treat performance as a design constraint that requires evidence.

* Choose the right algorithm before micro-optimizing.
* Choose the right data flow before micro-optimizing.
* Reduce wasted work before tuning small operations.
* Understand memory movement and allocation.
* Understand cache behavior, parallelism, and serialization costs.
* Keep setup work out of repeated execution paths.
* Measure performance-sensitive changes with representative inputs.
* Explain operation counts when benchmarks are impractical.
* Explain memory movement when benchmarks are impractical.

Do not claim speedups without evidence.
Evidence can be a benchmark, profile, or clear technical argument.
