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

## Task Modes

### Task Mode Selection

Universal principles apply to every coding task.
Select one primary task mode before editing.
Combine task modes when the work genuinely spans several modes.
* Use `Surgical Changes` for edits to existing code.
* Use `Bug Fixes` when correcting broken behavior.
* Use `New Features` when adding public behavior.
* Use `Refactors` when improving structure without behavior change.
* Use `Architecture Design` when shaping modules or interfaces.
* Use `Performance Work` when speed or resource use is the goal.
* Use `Documentation Work` when source behavior is not changing.

State the task mode when it affects tradeoffs.
Use the narrowest task mode that fits the request.

### Surgical Changes

Use surgical changes when editing existing code.
Touch only what the task requires.
Clean up only what your change makes obsolete.
* Avoid drive-by refactors.
* Do not improve adjacent code.
* Do not improve adjacent comments.
* Do not improve adjacent formatting.
* Do not refactor unbroken code unless asked.
* Match existing style even if you prefer another style.
* Preserve local naming for incremental edits.
* Remove artifacts made unused by your change.
* Mention unrelated dead code instead of deleting it.

Every changed line should trace to the task.

### Bug Fixes

Make bugs reproducible before fixing them when practical.
* Write a failing test that demonstrates the bug.
* Keep the failing test focused on the observed behavior.
* Make the test pass with the smallest safe change.
* Add regression coverage for the fixed behavior.
* Verify old behavior still works.
* Document behavior changes when users can observe them.

Do not fix one bug by creating another user-visible problem.

### New Features

Define the user-visible behavior before implementation.
* Specify the public contract.
* Specify inputs and outputs.
* Specify failure modes.
* Specify examples that should work.
* Add unit tests for local behavior.
* Add end-to-end tests or real examples for user workflows.
* Update docs for public behavior.

Do not add unrequested variants or configuration.
Add extension points only when current requirements need them.

### Refactors

Refactor to improve structure without changing public behavior.
* Identify tests that pass before the refactor.
* Preserve public behavior during the refactor.
* Keep mechanical moves separate from behavior changes when practical.
* Keep formatting churn inside the declared refactor scope.
* Update tests only when the public contract needs clearer coverage.

Do not mix hidden behavior changes into refactors.

### Architecture Design

Design architecture around invariants, boundaries, and verification.
* Define the domain model before choosing abstractions.
* Define input validation boundaries.
* Define pure kernels.
* Define I/O boundaries.
* Define lifecycle and ownership.
* Define error propagation.
* Define test seams.
* Define end-to-end examples.
* Define performance-sensitive paths.
* Define compatibility constraints.

Build input validation into boundary APIs.
Build unit tests into pure kernels.
Build end-to-end tests into user workflows.
Build performance measurements into performance-sensitive designs.

### Performance Work

Record the baseline before optimizing.
* Use representative inputs.
* Measure wall time.
* Measure memory when relevant.
* Measure allocation count when relevant.
* Measure throughput or latency when relevant.
* Note hardware assumptions when relevant.
* Note backend, compiler, and runtime assumptions when relevant.
* Keep expensive benchmarks out of fast default tests.
* Keep them in default tests only when the project already does.

Optimization is not done until the new measurement is recorded.

### Documentation Work

Prefer code that explains ordinary behavior.
Use docs for information that source cannot show clearly.

Document these things when they matter.
* Design choices.
* Algorithm derivations.
* Mathematical formulas.
* Units and coordinate conventions.
* Data schemas and file formats.
* Invariants.
* Ownership and cleanup rules.
* Concurrency assumptions.
* Performance tradeoffs.
* Compatibility constraints.
* Build, test, and release procedures.

Avoid these things.
* Comments that restate obvious syntax.
* Documentation that duplicates self-evident code.
* Marketing-only prose.
* Undocumented magic defaults.
* Stale examples.
* Hidden setup steps.

Keep docs close to the code they describe.
Update docs when public behavior changes.

## Computational Thinking

### Define The Model

Identify the model before implementing nontrivial behavior.
* Inputs and outputs.
* Mutable state.
* Required invariants.
* Error cases.
* Expected scale.
* Cost drivers.
* User-visible contract.

Ask before coding when the model is unclear.
Ask only after checking the code and docs.

### Separate Semantic Layers

Keep semantic layers distinct.
* Interface and user-facing API.
* Input validation.
* Unit and schema conversion.
* Pure computation.
* Backend or platform execution.
* Persistence and I/O.
* Visualization and reporting.
* Command-line or service entry points.

Small scripts may combine layers at the top level.
Reusable code should keep layers separate.

### Prefer Pure Kernels

Pure computation is easier to test and optimize.
Pure computation is easier to transform and reason about.
* Put pure logic in small functions.
* Pass required context explicitly.
* Keep I/O out of pure kernels.
* Keep global state out of pure kernels.
* Return values instead of mutating distant state when practical.
* Isolate unavoidable mutation behind narrow interfaces.

### Make Data Flow Inspectable

Design data flow so a reviewer can inspect it quickly.
* Where data comes from.
* Who owns it.
* When it is valid.
* How it is transformed.
* Where it is stored.
* How errors propagate.
* How resources are released.

Expose shape, stride, precision, alignment, and device placement.
Expose transfer points between memory, process, and device boundaries.

### State Tradeoffs

Record meaningful tradeoffs near the decision.
Use comments, docs, commit messages, or final explanations.
* Composability versus optimal batching.
* Memory footprint versus cached results.
* Startup cost versus repeated execution speed.
* Generic interface versus direct backend access.
* Compatibility versus cleanup.
* Strict input validation versus permissive migration.

Do not silently choose clever designs that change the contract.
