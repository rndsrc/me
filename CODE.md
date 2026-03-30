# Coding Guidelines

Guide load marker: `CODING-GUIDE-v0`.

This file is self-convergent.
Edits to this file should follow the rules declared in this file.
Higher-priority instructions still override this file.

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

### Verification by Design

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

### Performance with Evidence

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

### Define the Model

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

## Architecture Practices

### Public APIs

Keep public APIs small, stable, and meaningful.
* Expose domain concepts.
* Hide incidental implementation details.
* Avoid leaking temporary internal structure.
* Prefer small public surfaces with testable internals.
* Publish APIs only after understanding their lifetime.
* Update tests when public behavior changes.
* Update docs when public behavior changes.

Provide a migration path when compatibility matters.

### Abstractions

Add abstraction only when it earns its cost.

Good abstractions do at least one useful thing.
* Remove meaningful duplication.
* Represent a real domain boundary.
* Make testing easier.
* Isolate a backend or external dependency.
* Protect an invariant.
* Enable measurable performance or portability.

Weak abstractions often have these traits.
* They exist only for imagined future flexibility.
* They hide ownership, errors, or costs.
* They wrap a library without simplifying anything.
* They make compilers or reviewers see less.
* They spread one behavior across many files.

### Modules and Boundaries

Use modules to create clear ownership.
* Put reusable logic in library modules.
* Keep entry points thin.
* Keep backend-specific code behind narrow boundaries.
* Keep command-line parsing outside computational code.
* Keep file formats and protocols at edges.
* Avoid circular dependencies.

Split modules by semantic boundary.
Make construction, configuration, execution, and teardown explicit.
Use `mk*` and `rm*` pairs when local style supports them.
Use function-pointer interfaces for real module boundaries.
Use small protocol objects for real module boundaries.
Keep dynamic loading behind narrow interfaces.
Keep backend selection behind narrow interfaces.

### Data Ownership and Lifecycle

Make ownership clear for resources.
Resources include memory, files, handles, locks, tasks, and temp files.
* Pair acquisition with release.
* Prefer scoped resource management when the language supports it.
* Make cleanup paths easy to audit.
* Use cleanup labels in languages without automatic cleanup.
* Use cleanup helpers in languages without automatic cleanup.
* Avoid partial initialization unless teardown handles each state.

For shared data, document who may mutate it.
For shared data, document what synchronization protects it.

### Error Handling

Use error handling that matches the language and project.
* Perform input validation at boundaries.
* Use assertions for internal invariants.
* Do not use assertions for user input.
* Preserve original error context when wrapping errors.
* Do not swallow failures in setup.
* Do not swallow failures in I/O or numerical code.
* Do not swallow failures in release code.
* Avoid exiting inside reusable library functions.
* Keep error messages concise, specific, and actionable.

Function names and return conventions should agree.
Predicate functions should return booleans.
Action functions should return status, raise, or return result objects.
Follow local convention when choosing among those options.

### Configuration

Make configuration explicit and reproducible.
* Prefer command-line options when local convention uses them.
* Prefer config files when local convention uses them.
* Prefer environment variables when local convention uses them.
* Keep defaults documented.
* Add configuration only when users need to vary behavior.
* Avoid hidden behavior changes from ambient environment.
* Allow ambient behavior only when the project already does.
* Make generated or derived configuration inspectable.

### Dependencies

Treat dependencies as maintenance costs.
* Prefer the standard library.
* Prefer existing project dependencies.
* Add dependencies only when they remove real complexity.
* Add dependencies for costly, well-tested domain capabilities.
* Consider portability, install cost, licensing, and security.
* Consider long-term maintenance.
* Ask before adding production dependencies when policy is unclear.

### Generated Code and Artifacts

Use generated code only when it is part of the design.

When using generated code, make these facts clear.
* Source of truth.
* Generation command.
* Regeneration prerequisites.
* Expected generated outputs.
* Review boundary between generator and generated output.

Do not edit generated output by hand unless allowed.
Do not commit build products, caches, or temporary files.
Commit those files only when the project intentionally tracks them.

### Concurrency and Parallelism

Design concurrency deliberately.
* Identify shared state.
* Define ownership and synchronization.
* Avoid global mutable state.
* Keep critical sections small.
* Prefer immutable data when practical.
* Prefer message passing when practical.
* Test race-prone behavior with realistic concurrency.

For parallel numerical work, consider batching and vectorization.
For parallel data work, consider device transfer costs.
Also consider memory layout and determinism.

## Verification

Verification asks whether the work was built right.
Use checks to collect evidence that requirements are met.
Use tests to protect behavior, not implementation trivia.

### Check Layers

Choose checks by risk and behavior surface.
* Use unit tests for local behavior.
* Use integration tests for cross-module data flow.
* Use end-to-end tests or real examples for important workflows.
* Use regression tests for bug fixes.
* Use property tests when many cases matter.
* Use invariant checks when invariants matter.
* Use numerical reference checks for scientific code.
* Use CLI or service smoke checks for entry points.
* Use builds, type checks, and lint for project-level feedback.
* Use benchmarks for performance claims.
* Use diff review to find unrelated churn.

### Verification Goals

Define success as evidence that can be checked.
* Bug fix: failing case passes and old behavior remains intact.
* Feature: public behavior matches the documented contract.
* Refactor: relevant checks pass before and after.
* Refactor: public behavior is unchanged.
* Performance work: measured cost decreases on representative inputs.
* Documentation work: examples, commands, and procedures are accurate.

### Verification Loops

Turn each task into a verifiable goal before coding.
Loop until the goal has evidence or a real blocker is found.
* Input-validation work: check valid and invalid boundary cases.
* Bug fix: reproduce the observed failure with a test first.
* Feature: check user-visible behavior directly.
* Refactor: run behavior checks before and after.
* Performance work: record the baseline before changing code.
* Documentation work: run or inspect changed examples and commands.

Weak goals such as `make it work` require clarification.
Strong goals let the agent verify progress independently.

### Numerical and Data Checks

For numerical or data-heavy code, check data meaning directly.
* Units and dimensions.
* Shapes, broadcasting rules, and layouts.
* Dtypes, precision, and tolerances.
* Empty inputs and boundary cases.
* Singularities and near-zero cases.
* Error bounds.
* Analytical identities.
* Reference values.
* Conservation properties.

Document non-obvious tolerance choices.

### Definition of Done

Finish only after relevant checks are complete.
* Run the relevant checks.
* Inspect the diff for unrelated churn.
* Check for accidental generated files.
* Report checks that could not run.
* Report remaining behavior or compatibility risks.

Do not claim completion when relevant checks were skipped.

## Git History

Commit history is part of the project.
Keep history clean, useful, and reviewable.

### Commit Shape

Use one commit per logical change.
* Separate fixes from optimizations.
* Separate behavior changes from formatting.
* Separate refactors from behavior changes when practical.
* Separate mechanical moves from edits to moved code.
* Separate generated output from generator changes when practical.
* Separate dependency updates from behavior changes when practical.
* Keep each commit reviewable.
* Keep each commit buildable when practical.

Do not rewrite user commits unless asked.
Do not squash user history unless asked.

### Commit Messages

Write useful imperative commit messages.

Good subjects start with verbs such as these.
* `Add ...`
* `Fix ...`
* `Use ...`
* `Remove ...`
* `Refactor ...`
* `Document ...`
* `Bump ...`
* `Release ...`

Good commit bodies explain what matters.
* The problem.
* The user-visible effect.
* The implementation choice.
* Tradeoffs or compatibility notes.
* Tests or benchmarks run.

Avoid vague subjects such as `misc`, `updates`, or `cleanup`.
Avoid vague subjects such as `fix stuff`.

### Review Discipline

Make each change easy to review.
* Keep the purpose narrow.
* Include tests or explain why tests are not appropriate.
* Avoid unrelated formatting churn.
* Preserve local style.
* Explain non-obvious tradeoffs.
* Leave the repository reproducible.

## General Programming Style

### Local Style Versus Defaults

Use local style for incremental edits.
Use this guide for new code when local rules are absent.
Use this guide for refactors when local rules are absent.
Use this guide for new projects when local rules are absent.

For incremental edits, keep formatting churn minimal.
For refactors, format the declared refactor scope consistently.
Separate behavior changes from pure style changes when practical.

### Formatting

Use simple, consistent formatting.
* Use UTF-8 and LF line endings.
* Use ASCII-only text unless the project or task requires Unicode.
* End files with a newline.
* Remove trailing whitespace.
* Keep lines at or under 79 columns.
* Put each sentence on its own physical line in policy docs.
* Use blank lines to separate concepts.
* Do not add editor modelines to source files.

Use the project's formatter when one is configured.
Do not introduce a new formatter as a side effect.

### Naming

Choose names by scope, lifetime, and meaning.
* Short local names are acceptable when scope is small.
* Short local names are acceptable when meaning is obvious.
* Wider-scope names should be longer and more descriptive.
* Public names should describe domain meaning.
* Public names should not describe implementation mechanics.
* Module, file, class, and type names should describe stable concepts.
* Function names should describe the action, result, or predicate.
* Predicate names should read like boolean questions or properties.
* Variable names should describe the value's role.
* Mathematical code may use conventional short symbols.
* Use short symbols only when context makes them clear.
* Avoid clever abbreviations in public APIs.
* Avoid encoding incidental types into names.
* Use paired names consistently.
* Prefer pairs such as `current` and `next`.
* Prefer pairs such as `old` and `new`.
* Use domain equivalents when they are clearer.

Rename unclear code when the rename is in scope.
Do not churn public names without a compatibility plan.

### Signature Conventions

Use CK signature conventions when local style is absent.
Use them when adding to CK-style modules.
Preserve stronger local conventions in existing projects.
* Use `mk*` for factories, constructors, and allocation functions.
* Use `rm*` for destructors, release functions, and teardown functions.
* Keep `mk*` and `rm*` names paired for the same resource.
* Use domain names for public mathematical functions.
* Use domain names when construction is not the main idea.
* Use capitalized factory names for conceptual components.
* Use short method names inside vtables.
* Use short method names when the receiver supplies the namespace.
* Use longer free-function names when no receiver gives context.

For Lux-style C interfaces, use these conventions.
* Use `Lux_class` for public Lux handle or object types.
* Use `struct Lux_class_s` for exposed backing struct tags.
* Use `lux_method` for public Lux functions.
* Use lower-case method fields such as `exec`, `load`, `mk`, and `rm`.
* Use function-pointer interfaces for modules, resources, tasks, plugins.

Do not force these names into projects with another clear naming scheme.

### Functions

Keep functions focused.
* Do one thing well.
* Keep argument lists short enough to understand.
* Use helpers when indentation grows too complex.
* Use helpers when local state grows too complex.
* Avoid boolean flags that drastically change behavior.
* Prefer separate functions for different behavior.
* Prefer explicit modes for different behavior.
* Make side effects visible in names, return values, or APIs.

### Data Structures

Choose data structures that make invariants clear.
* Prefer named fields over positional tuples.
* Use positional tuples only when values have the same meaning.
* Prefer immutable values for shared data when practical.
* Keep conversion at boundaries.
* Avoid passing loose dictionaries through many layers.
* Make optional values explicit.
* Make missing states explicit.

### Imports and Includes

Keep dependencies readable.
* Group standard library, third-party, and local imports.
* Avoid wildcard imports unless local style uses them.
* Remove imports made unused by your change.
* Remove includes made unused by your change.
* Do not reorder unrelated imports without a project formatter.

### Tables and Repeated Cases

Use table-driven code when many cases share behavior.

Use tables when cases differ only by constants, names, or flags.
Use tables when a switch encodes data instead of behavior.
Use explicit branches when cases have different algorithms.

## Language-Specific Style

### Python

Use local Python style first.
Use these defaults when local rules are absent.

For new CK-style Python packages, use `mod/<package>`.
Do not use `src/<package>` unless the project already uses `src`.
Use `src` when the user explicitly asks for it.
Configure packaging so the package root points at `mod`.
Use `packages = [{include = "<package>", from = "mod"}]` for Poetry.
Use `find_packages("mod")` for setuptools packages.
Use `package_dir={"": "mod"}` for setuptools packages.
* Use 4 spaces for indentation.
* Prefer explicit imports.
* Use type hints at public boundaries when they clarify contracts.
* Keep pure computation separate from I/O.
* Use `dataclass`, `NamedTuple`, or small classes for structured state.
* Use exceptions for invalid external input.
* Use assertions for internal invariants.
* Write direct unit tests unless local convention differs.
* Use `mk*` for lower-case factories.
* Use `mk*` when construction is the main idea.
* Use capitalized factory names such as `Step`, `Engine`, or `Dense`.
* Use capitalized factory names for conceptual components.
* Use short mathematical locals such as `t`, `T`, `x`, `X`, and `h`.
* Use short mathematical locals such as `H`, `i`, and `r`.
* Use short names only when equations make them clear.
* Use `u_` prefixes for unit-bearing arguments when local style uses them.

For numerical Python, keep units and backend setup at boundaries.
Keep array kernels backend-friendly when practical.
Avoid Python loops in hot array code unless intentional.
Test shapes, dtypes, tolerances, and transformations.

### C, C++, CUDA, and Systems Code

Use local systems style first.
Use these defaults when local rules are absent.
* Use K&R-style control blocks for new C-like modules.
* Use tabs for indentation when no local rule exists.
* Keep public symbols descriptive.
* Keep local variables concise when scope is small.
* Use `Lux_class` and `lux_method` in Lux-style public interfaces.
* Use `mk*` and `rm*` pairs for constructors and destructors.
* Use `static` for private helpers.
* Prefer `static inline` over function-like macros.
* Use macros for constants.
* Use macros for compile-time genericity.
* Use macros for zero-cost patterns that C cannot express cleanly.
* Avoid macros when the language can express the idea cleanly.
* Check allocation failures.
* Check system-call failures.
* Make ownership and cleanup paths explicit.
* Keep conditional compilation out of core logic when possible.
* Isolate device-specific code behind narrow interfaces.
* Isolate backend-specific code behind narrow interfaces.

Follow these macro rules.
* Parenthesize arguments and expressions.
* Avoid multiple evaluation.
* Avoid hidden control flow.
* Avoid dependence on magic local variable names.
* Use `do { ... } while (0)` for multi-statement macros.

### Shell Scripts

Use local shell style first.
Use these defaults when local rules are absent.
* Prefer POSIX shell when portability matters.
* Use Bash only when Bash features are needed.
* Quote variables unless word splitting is intentional.
* Fail clearly on missing commands or bad arguments.
* Use temporary files safely.
* Keep scripts composable from other scripts and CI.
* Document environment variables and required tools.

Use `set -e` only when the script handles its edge cases.
Use stricter modes only when the script handles their edge cases.
Do not add strict mode blindly to sourced scripts.
Do not add strict mode blindly to complex pipelines.

### Build, Config, and CI Files

Keep build and CI behavior reproducible.
* Keep build commands documented.
* Keep generated files out of source unless deliberately tracked.
* Prefer standard project tooling over custom scripts.
* Do not change release workflows in unrelated code work.
* Do not change publish workflows in unrelated code work.
* Keep CI job names descriptive.
* Keep dependency updates separate from behavior changes when practical.

### Documentation and Markdown Files

Use local documentation style first.
Use these defaults when local rules are absent.
* Use clear headings.
* Use `*` for bullets in Markdown governed by this guide.
* Keep examples runnable.
* Put each sentence on a new line in policy docs.
* Use code fences with language names.
* Separate user instructions from developer instructions.
* Document limitations explicitly.
* Avoid stale badges, stale commands, and hidden prerequisites.

## Agent Checklist

Before editing, confirm these facts.
* The real goal.
* The public contract affected.
* The relevant local style.
* The task mode.
* The smallest safe change.
* The verification steps.

While editing, follow these rules.
* Keep the diff focused.
* Preserve local style for incremental changes.
* Use this guide's defaults for new or refactored code.
* Keep state, ownership, and units explicit.
* Avoid speculative abstraction.
* Update tests and docs when behavior changes.

Before finishing, complete verification.
* Run relevant tests.
* Run relevant build checks.
* Run relevant type checks.
* Run relevant lint checks.
* Inspect the diff.
* Remove accidental generated files.
* Confirm clean commit boundaries when committing.
* Report verification and residual risk.
