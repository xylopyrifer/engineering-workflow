---
name: engineering-workflow
description: Plan and deliver maintainable software, automation, data, and content projects. Use for new projects, feature development, bug fixes, and refactoring to clarify requirements and impact, define architecture and contracts, and implement in proportionate stages. Do not apply the full workflow to ordinary questions, translations, or standalone short writing.
---

# Engineering Workflow

## Core Principles

Define the problem before designing the system. Establish conventions before implementation. Build a stable foundation before adding features and content. Deliver work that is easy to understand, verify, modify, and extend.

- Evaluate each task against the project goals, existing architecture, and user journey. Avoid accumulating isolated patches.
- When requirements or direction are unclear, investigate and design first. Reading files, inspecting the current state, and running small experiments with explicit validation goals can proceed immediately.
- Match engineering rigor to the project's size, risk, and expected lifetime. Preserve boundaries for known extensions without introducing microservices, plugin systems, or layers of abstraction for hypothetical needs.
- Explicit user instructions take priority. Follow existing project conventions and other applicable skills. This skill organizes the engineering process; it does not replace domain-specific standards.
- Stage exit criteria are self-checks, not requests for user approval at every stage. When direction and authorization are clear, continue through delivery. Ask only for missing information that materially affects goals, scope, or irreversible decisions, while advancing work that does not depend on the answer.

## 1. Understand the Current State and Choose the Depth

Read project instructions, relevant documentation, directory structure, configuration, dependencies, and validation entry points. For an existing project, inspect current changes and protect the user's unfinished work.

| Task type | Required depth |
| --- | --- |
| New project or complex feature spanning modules | Follow all stages and maintain written requirements, architecture, conventions, and acceptance evidence. |
| Iteration or refactoring in an existing project | Reuse existing conventions. Assess effects on callers, data, configuration, compatibility, and tests; document only what changes. |
| Small fix or adjustment | Briefly state the problem, impact, approach, and acceptance criteria before implementation. Stages may be combined; a new design document is optional. |
| Explicitly requested disposable prototype | Use minimal structure. Identify simplifications and conditions for production use; keep the prototype distinct from the maintained implementation. |

For non-software projects, interpret modules as content or workflow units, and interfaces as inputs, outputs, and handoff criteria. Do not invent API, code, or production layers when they do not exist.

## 2. Clarify Requirements

Create a requirements summary proportionate to the task:

- **Goals and users:** Whose problem is being solved, and in what setting?
- **Scope and priorities:** What is required, optional, and explicitly out of scope?
- **Inputs and outputs:** Where does data or content come from? What is delivered, and how will it be used?
- **Constraints:** Identify relevant existing systems, runtime environments, budget, time, permissions, privacy, performance, and compatibility requirements.
- **Acceptance:** Turn terms such as "usable," "reliable," and "extensible" into observable behaviors or checks, including critical failure paths.
- **Open questions:** Distinguish facts, assumptions, conflicts, and blockers. Explain which decisions they affect. State assumptions and proceed with low-risk, reversible choices.

**Exit criteria:** Explain why the work matters, what will be built, and how completion will be assessed. No blocking ambiguity remains in the core direction. Put future ideas in a follow-up list without automatically expanding the current scope.

## 3. Design the Product, Technical Approach, and Architecture

- Describe the main user journey and key states, then choose the simplest maintainable approach that supports them.
- Compare reasonable alternatives when meaningful tradeoffs exist. Record the rationale, costs, and conditions for revisiting the decision. Routine choices do not need lengthy justification.
- Define module responsibilities, directory organization, dependency direction, data flow, state ownership, and external system boundaries. Avoid ambiguous ownership, circular dependencies, and unrestricted access to shared mutable state.
- Reuse the existing architecture and fix root causes in the appropriate module. If architectural change is necessary, explain the impact and incremental migration path first. Keep unrelated refactoring out of scope.
- Identify the most important technical uncertainty early. When needed, run a minimal experiment in an isolated location and record the conclusion. Do not treat experimental code as the production foundation without review and adaptation.

**Exit criteria:** Every core requirement has a clear owner, key data flows can be explained, and the design supports known next steps.

## 4. Establish Conventions Before Implementation

Define the relevant conventions before implementation. Reuse existing ones and fill actual gaps.

### Code and Dependencies

- Use consistent naming, directories, module exports, dependency direction, and formatting. Define how runtime and dependency versions are managed.
- Place business rules, external integrations, and presentation responsibilities behind appropriate boundaries. Avoid duplicated logic, magic values, implicit dependencies, and names that convey no meaning.
- Define input validation, exception propagation, recoverable errors, and user-facing messages. Include enough context in logs to diagnose problems without recording secrets or unnecessary personal data.
- Use comments to explain reasons, constraints, and non-obvious decisions. Document how to run, configure, validate, and modify the project instead of restating code line by line.

### Interfaces and Data Contracts (When Communication Is Involved)

- Specify data models, field types, required and nullable fields, defaults, units, and time formats.
- Define inputs, outputs, success and error examples, error codes or equivalent error types, and caller handling.
- Specify authentication, pagination, timeouts, retries, idempotency, and concurrency only where the actual requirements call for them.
- Define versioning and compatibility. For breaking changes, identify affected callers, migration steps, and rollback paths. Consider how older readers behave even when adding optional fields.
- Keep contracts in one authoritative location appropriate to the project, such as type definitions, schema files, or an API specification. Avoid drift between manually duplicated definitions.

### Configuration

- Provide a unified configuration entry point, organized by responsibility, for the environments, paths, service endpoints, model parameters, and business parameters actually used.
- Specify source precedence, types, defaults, and startup validation. Missing required configuration should produce actionable errors instead of silently falling back to the wrong environment.
- Separate committable configuration, environment-specific values, and secrets. Provide examples without real secrets. Avoid hardcoding environment-specific values; fixed business constants may be centrally named.

### Validation Strategy

- Map core acceptance criteria to appropriate automated or manual checks, covering critical behavior, interface boundaries, and failure paths.
- Prefer the existing test framework. Do not add tests that merely repeat the implementation for reversible, low-impact changes.
- Provide appropriate recovery plans and validation methods for data migrations or high-impact changes.

**Exit criteria:** An implementer does not have to guess module boundaries, interface formats, configuration sources, or passing criteria.

## 5. Build the Foundation and Core Implementation

1. Create the necessary directories, configuration entry point, module boundaries, and run and validation entry points. Avoid empty layers without a concrete purpose.
2. Establish a minimal end-to-end path to confirm that the main modules work together. Clearly label mock data and placeholder implementations in demonstrations and deliverables.
3. Implement core features in priority order, then complete content, interactions, and edge cases. Keep every completed increment runnable, verifiable, and ready for continued development.
4. When new evidence invalidates the design, update the relevant decisions and impact assessment before changing the implementation. Revise the design based on evidence without silently diverging from contracts.
5. Bound necessary temporary measures and document their reasons, risks, and removal conditions. Do not substitute an unexplained workaround for a root-cause fix.

## 6. Validate, Optimize, and Deliver

- Run the necessary checks proportionate to the change, verify acceptance criteria, and fix discovered problems. Clearly state which checks were not run or were blocked by the environment.
- Optimize in response to observed bottlenecks, defects, or acceptance requirements. Do not add complexity based on speculation.
- Update affected interfaces, configuration examples, usage instructions, and important design records so that documentation matches the final implementation.
- Include completed behavior, key tradeoffs, usage instructions, validation results, known limitations, and follow-up recommendations in the handoff. Recommendations must not disguise unfinished commitments in the current scope.
- For long tasks, maintain a concise project status covering completed work, the current stage, open questions, and the next executable step. Avoid copying the same status into multiple documents.

**Completion criteria:** The agreed scope is implemented; relevant checks pass or limitations are honestly documented; interfaces and configuration have no unintended breakage; and the handoff supports the next round of changes.

## Documentation and Iteration

Prefer updating existing documentation. A new long-lived project may use one design document for goals, scope, acceptance, architecture, interfaces, configuration, stages, and decisions. Split it only when the content is complex enough to justify separate maintenance. Do not create an empty file for every heading.

For each subsequent change, repeat: understand the current state and requirements, assess impact, update necessary design and conventions, implement, validate, and synchronize documentation. Complete the current task before recording technical debt and next-stage recommendations.
