---
title: "AGENTS"
version: "0.1.0"
author: "Double FW"
date: "2026-10-13"
license: "See LICENSE"
language: "en"
repository: "Double-FW/Accessible-Design-Code-and-Testing-RAG-Template"
artifact_type: "policy_document"
use_case:
  - "accessibility-first-code-generation"
  - "pipeline-integration"
  - "human-in-the-loop-escalation"
entities:
  - "design-system"
  - "behavior-contract"
  - "component"
  - "automated-test"
  - "manual-test"
  - "human-review"
---

```yaml name=agents-metadata.yml
# Machine-readable policy block: agents should parse this reliably.
policy_versioning:
  version: "0.1.0"
  last_reviewed: "2026-10-13"
  reviewers:
    - name: "Double FW"
      role: "owner"
  changelog:
    - date: "2026-10-13"
      changes: "Initial machine-readable metadata, observability and templates added."
      author: "Double FW"
observability:
  audit_events:
    - "behavior_contract.created"
    - "implementation.generated"
    - "test.run"
    - "human_review.opened"
    - "human_review.resolved"
  retention_days: 365
  redact_fields:
    - "user_email"
    - "personal_data"
  export_format: "jsonl"
  required_fields_for_escalation:
    - "task_id"
    - "artifact_path"
    - "evidence_url"
machine_rules:
  require_yaml_front_matter: true
  require_behavior_contract_before_code: true
  treat_axe_as_evidence_not_proof: true
  escalate_on_missing_label_meaning: true
```

```json name=decision-graph.json
{
  "start": "intake",
  "nodes": {
    "intake": { "next": "grounding", "action": "collect-config" },
    "grounding": {
      "action": "validate-sources",
      "on_missing": "request_human_input",
      "next": "behavior_contract"
    },
    "behavior_contract": { "action": "emit-contract", "next": "implement" },
    "implement": { "action": "generate-code-and-tests", "next": "validate" },
    "validate": {
      "action": "run-automated-tests",
      "on_failure": "open_human_review",
      "next": "report"
    },
    "report": { "action": "publish-report", "end": true },
    "request_human_input": { "action": "emit-human-prompt", "next": "wait_for_human" }
  }
}
```

```yaml name=templates.yml
# Short, templated prompts and response payloads agents can emit and parse.
prompts:
  behavior_contract_request: |
    BEHAVIOR-CONTRACT-REQUEST:\
    component={{component_name}}; scope={{scope}}; required_states={{states}}; expected_roles={{roles}}
  human_review_notification: |
    HUMAN_REVIEW: id={{id}}; reason="{{reason}}"; severity={{severity}}; fields={{fields}}; evidence_url={{evidence_url}}
responses:
  behavior_contract_response: |
    BEHAVIOR-CONTRACT: name={{name}}; role={{role}}; keyboard={{yes/no}}; focus={{focus_summary}}; states={{json_states}}; notes={{notes}}
  human_decision_response: |
    HUMAN_DECISION: id={{id}}; decision={{approve|revise|reject}}; replacement_text={{text}}; reviewer={{name}}
```

# AGENTS.md

## Purpose

This repository is a governance and workflow template for AI-assisted, accessibility-first design and code generation. Agents working here or with this template should behave like pipeline integrat[...]

The project’s priority is to preserve design-system intent, generate accessible behavior correctly, and avoid claiming compliance without evidence. This includes being explicit when human review [...]

## Core responsibilities

Agents in this repository must:

- integrate project context, design-system rules, brand constraints, and accessibility requirements into one coherent generation pipeline;
- manage work as a staged process instead of a single free-form code generation step;
- produce implementation and evidence together, not code without validation;
- keep traceability between requirements, decisions, code, tests, and residual risk;
- flag uncertainty and request human input when labels, names, wording, or contextual meaning cannot be verified from available evidence.

## Operating model

### 1. Intake and configuration

Before generating design or code, the agent should:

- confirm the relevant framework, design system, tokens, and repository conventions;
- capture scope, assumptions, and constraints; 
- load the configured accessibility template or project governance document;
- identify any unknown or missing project inputs and keep them visible as unresolved instead of fabricating them.

Required fields to resolve or explicitly mark as unknown include:

- JavaScript framework and version;
- UX design system and component catalogue;
- brand and content rules;
- design tokens and interaction expectations;
- supported browsers, devices, and assistive technologies;
- test runner and axe version;
- escalation responsibility and review owners.

### 2. Source grounding and decision capture

Agents should prefer approved local sources and explicit project rules over general solutions. The hierarchy should be:

1. project design system and brand rules;
2. framework conventions and repository standards;
3. native HTML and platform semantics;
4. approved accessibility guidance and pattern references;
5. local exceptions or documented constraints.

When a rule or pattern conflicts with accessibility outcomes, the agent must record the conflict and escalate rather than silently choose a weaker option.

### 3. Behavior contract before implementation

For every UI component or flow, state the expected behavior clearly before generating code. Include:

- role and purpose;
- required keyboard behavior;
- focus management;
- state transitions;
- expected accessible name, role, value, and state;
- visible and non-visible instructions or labels;
- interaction assumptions and edge cases.

A generated component without a behavioral contract is incomplete.

### 4. Code generation rules

When generating code:

- prefer native HTML and platform semantics over custom ARIA widgets;
- preserve design-system patterns and approved branding where they support accessibility;
- avoid introducing competing local patterns when a design-system component already exists;
- implement state, focus, and error handling explicitly;
- ensure labels, names, and textual equivalents are meaningful and aligned to the user task;
- keep generated code traceable to the behavior contract and source decisions.

### 5. Automated and manual testing

Every generated artifact should be paired with evidence. Required testing includes:

- automated accessibility checks using the pinned axe configuration;
- behavioural assertions for keyboard, focus, and state changes;
- manual checks for visible labels, structure, focus visibility, zoom, reflow, and error recovery;
- explicit assistive-technology escalation for complex widgets or risky interactions.

Do not treat an axe pass as proof of WCAG conformance on its own.

### 6. Reporting and evidence capture

Project output should include a proportionate report containing:

- scope and assumptions;
- source and pattern decisions;
- accessible behavior contract;
- implementation summary;
- automated test evidence;
- manual test evidence;
- coverage and traceability matrix;
- known limitations and residual risk;
- escalation needs for assistive-technology testing.

Reports must be explicit about what is known, verified, unknown, and unverified.

## Human-in-the-loop requirements

Human input is required whenever meaning or context cannot be reliably inferred. Flag these cases immediately and stop short of claiming correctness when the answer depends on human judgement.

Examples include:

- whether a label, instruction, or textual equivalent is meaningful to the target users;
- whether a visible or hidden label accurately reflects the UI’s purpose;
- whether a custom accessible name is business-accurate rather than merely technically valid;
- whether a content choice is appropriate for a given audience, brand tone, or compliance expectation;
- whether a design-system or brand decision conflicts with accessibility goals and requires product approval;
- whether a complex interaction or custom widget requires real assistive-technology validation.

When in doubt, the agent should produce a report entry like:

- `HUMAN REVIEW REQUIRED: label text meaning and user clarity must be confirmed.`
- `HUMAN REVIEW REQUIRED: contextual equivalence for this control cannot be verified from source text alone.`
- `HUMAN REVIEW REQUIRED: assistive-technology validation is required for this custom interaction.`

## Pipeline integration expectations

Agents should manage work as a pipeline rather than a one-shot prompt:

1. define task and constraints;
2. gather canonical sources;
3. convert requirements into a behavior contract;
4. generate implementation;
5. generate tests;
6. validate findings;
7. report results and open human-review items;
8. preserve decision history and residual risks.

The same project should keep the design rationale, implementation, and evidence together so decisions remain auditable.

## Required output posture

The agent must:

- state assumptions explicitly;
- distinguish WCAG requirements from design-system preferences and best practices;
- avoid false certainty;
- treat unknowns as unknown until resolved;
- surface gaps in evidence and ask for human confirmation when required.

## Quality bar

Before concluding a task, the agent should confirm:

- the implementation matches the stated accessibility behavior contract;
- the relevant tests exist and are relevant to the behavior;
- labels, names, and textual equivalents are meaningful and contextually correct;
- unresolved questions have been surfaced for human review;
- no compliance claim is made without supporting evidence.

## Repository-specific note

This repository is a template for governance and AI-assisted generation. When working inside it, prefer durable, reusable process guidance over incidental prompt-level fixes. The goal is repeatab[...]

## Summary

Agents operating in this repository should behave as accessibility-aware orchestrators: they must integrate sources, generate code and tests together, maintain traceability, and escalate to human[...]

This is especially important for labels, instructions, textual alternatives, and business context where a technically plausible result may still be semantically wrong or inaccessible to the user.
