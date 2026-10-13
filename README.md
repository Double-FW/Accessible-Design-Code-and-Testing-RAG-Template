# Accessible-Design-Code-and-Testing-RAG-Template
A reusable RAG template that guides AI to generate accessible designs, code and tests, from atomic elements to complete websites. It preserves brand and design-system choices while applying WCAG 2.2 A/AA, axe automation, manual testing and evidence-based conflict resolution.

> NOTE: This repository now includes AGENTS.md — a machine-friendly and human-guidance policy that defines how agents (automated systems and human+AI teams) should operate when using this template. Read AGENTS.md before integrating any agentic workflows.

## What this repository contains

The core document is:

- [`Accessible_Generation_and_Testing_RAG_Template.md`](./Accessible_Generation_and_Testing_RAG_Template.md)
- [`AGENTS.md`](./AGENTS.md)
- [`LICENSE`](./LICENSE)

The repository is designed to be used as a persistent knowledge and governance document for AI-assisted design or development work. Once configured, it applies a consistent accessibility approach to generated design, code and tests.

## Why AGENTS.md was added

AGENTS.md extends the original template by providing:

- YAML front matter and machine-readable policy metadata that automation can parse,
- prompt and response templates for structured agent behaviour,
- observability and audit rules for escalations and evidence capture,
- a quick-start checklist and a minimal decision flow for programmatic pipelines,
- versioning, review and changelog metadata that can be checked before trusting rules.

This makes it practical for human+AI teams to run repeatable, auditable accessibility workflows and to shift accessibility left in development pipelines.

## How to complete this template: human, AI, or hybrid

The template must be configured with project-specific values before use. The following completion paths are valid, and they can be combined:

### 1. Human-first completion

- Copy `Accessible_Generation_and_Testing_RAG_Template.md` to a configured project file such as `configured/Accessible_Generation_and_Testing_RAG_Project.md`.
- Replace all `{{PLACEHOLDER_FIELDS}}` with confirmed project information.
- Include the project’s framework, design system, tokens, testing stack, browser matrix, product context and escalation owner(s).
- Maintain a changelog, decision log and exception register.

### 2. AI-assisted completion

- Give the AI agent access to the project documentation, design-system sources, brand rules, repo conventions and existing tests.
- Load AGENTS.md and the configured template as persistent context.
- Ask the agent to draft the configured file, propose behavior contracts, and identify unresolved fields.
- Require human validation for any field that depends on product meaning, brand interpretation or accessibility judgement.

### 3. Hybrid completion (recommended)

This is the most effective model for mature accessibility programmes:

- let the AI draft the configuration, behavior contract and implementation skeleton;
- let human reviewers confirm contextual meaning, labels, wording, and business-approved content;
- let the AI generate tests and evidence artefacts;
- let humans approve the final output or request escalation when real assistive-technology validation is needed.

The important rule is that no automated system should treat a human-sensitive decision as resolved without explicit human approval.

## Recommended workflow for human + AI engineering teams

### 1. Intake and configuration

Before generating design or code, the team should:

- confirm framework, design system and repository conventions;
- capture scope, assumptions and constraints;
- load AGENTS.md and the configured accessibility template into the agent context;
- identify unknown or unresolved project inputs and keep them visible rather than inventing them.

This should include:

- JavaScript framework and version;
- UX design system and component catalogue;
- brand and content rules;
- design tokens and interaction expectations;
- supported browsers, devices and assistive technologies;
- test runner and pinned axe version;
- escalation responsibilities and review owners.

### 2. Contract before implementation

For each UI element, component or journey, the AI should create a behaviour contract before code is generated. The contract should include:

- purpose and role;
- keyboard behaviour;
- focus management;
- state transitions;
- expected accessible name, role, value and state;
- visible and non-visible instructions or labels;
- assumptions and edge cases.

A component without a behaviour contract is incomplete.

### 3. Generation and design-system alignment

AI-generated output should:

- prefer native HTML and platform semantics before ARIA or custom widgets;
- preserve approved design-system patterns and brand rules where they support accessibility;
- avoid creating competing local patterns when an approved pattern already exists;
- keep implementation traceable to source decisions and the behaviour contract.

### 4. Validation and evidence

Every generated feature should be paired with evidence, including:

- automated accessibility checks using the pinned axe configuration;
- behavioural assertions for keyboard interaction, focus management and state changes;
- manual checks for visible labels, structure, focus visibility, zoom, reflow and error recovery;
- escalation to assistive-technology testing when a custom widget or critical journey creates a material risk.

Do not treat an axe pass as proof of WCAG conformance on its own.

### 5. Human review and escalation

Human input is required whenever meaning or context cannot be inferred reliably. The team should explicitly flag these items and stop short of claiming correctness when the answer depends on human judgement.

Examples include:

- whether a label, instruction or textual equivalent is meaningful to its target users;
- whether a visible or hidden label accurately reflects the interface’s purpose;
- whether an accessible name is business-accurate rather than just technically valid;
- whether a design-system or brand decision conflicts with accessibility goals and needs product approval;
- whether a complex interaction requires assistive-technology validation.

### 6. Monitoring and reporting for accessibility programmes

To improve monitoring and reporting for accessibility programmes, the team should capture structured audit events, evidence and review outcomes across projects. The following are recommended:

- Log structured events for behavior contracts, implementation generation, test runs, human reviews and test outcomes.
- Keep evidence artefacts alongside the PR, issue or evidence register, including automated reports, screenshots and manual-test notes.
- Maintain a review register for human actions and decisions.
- Track patterns across projects, including recurring failure types and unresolved accessibility risks.
- Publish a small set of programme metrics to product and accessibility stakeholders:
  - percentage of generated artefacts with complete behaviour contracts;
  - percentage of PRs with automated accessibility checks;
  - pass/fail trend for axe rule sets;
  - number of open human-review items;
  - average time to resolve review items;
  - number of critical journeys requiring AT testing.

This supports a shift-left model: accessibility work starts earlier and becomes visible earlier in the pipeline rather than being delayed until a late-stage audit.

## Quick-start checklist

- [ ] Copy the template into a configured project file.
- [ ] Load `AGENTS.md` into the agent or RAG context.
- [ ] Confirm framework, design system, brand constraints and supported platforms.
- [ ] Generate a behaviour contract before implementation.
- [ ] Run automated accessibility and behavioural tests in CI.
- [ ] Open human-review items for any contextual or label ambiguities.
- [ ] Retain evidence and audit logs for each generated artefact.
- [ ] Review accessibility metrics regularly with engineering and product owners.

## Versioning, changelog and trust checks

`AGENTS.md` includes version, review and changelog metadata so automation can validate that the policy is current before acting on it. When repository rules change, the version should be incremented and the changelog updated.

This allows engineering teams to build guardrails into their pipelines instead of relying on ad hoc prompting.

## Governance and ownership

The template works best when ownership is shared across:

- accessibility;
- design systems;
- brand and content;
- frontend engineering;
- quality assurance;
- product governance.

One named owner should remain accountable for versioning and review, while domain owners approve changes that affect their systems.

## Status

This README describes the configured operational use of the template. It is intended to support both human-led and AI-assisted work, and to make accessibility evidence visible early in the engineering lifecycle rather than as a last-step compliance activity.

For more details, read:

- [`Accessible_Generation_and_Testing_RAG_Template.md`](./Accessible_Generation_and_Testing_RAG_Template.md)
- [`AGENTS.md`](./AGENTS.md)

---

## Licence

Add the licence appropriate to the organisation and repository.

`{{LICENCE_NAME_AND_LINK}}`

Check the individual terms of referenced external sources before reproducing their examples. Linking to guidance does not transfer its licence to this project.
