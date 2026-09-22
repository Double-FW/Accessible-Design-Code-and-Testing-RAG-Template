# Accessible-Design-Code-and-Testing-RAG-Template
A reusable RAG template that guides AI to generate accessible designs, code and tests, from atomic elements to complete websites. It preserves brand and design-system choices while applying WCAG 2.2 A/AA, axe automation, manual testing and evidence-based conflict resolution.

## What this repository contains

The core document is:

- [`Accessible_Generation_and_Testing_RAG_Template.md`](./Accessible_Generation_and_Testing_RAG_Template.md)

It is designed to be used as a persistent knowledge and governance document for an AI-assisted design or development conversation. Once configured, it applies a consistent accessibility approach to every interface artefact generated during that chat or workflow.

The template can govern work at different levels of scale:

- a single HTML element;
- a component or interaction pattern;
- a page or application view;
- a multi-step user journey;
- a complete website or web application;
- the automated and manual tests associated with any of the above.

## Why it exists

AI systems can generate code that looks plausible while missing important accessibility behaviour. They may also:

- treat an automated axe scan as proof of WCAG conformance;
- apply ARIA without implementing the associated keyboard behaviour;
- replace an organisation’s approved design patterns with generic examples;
- overlook loading, error, disabled and expanded states;
- blur the distinction between WCAG requirements and useful best practices;
- claim to have tested a screen-reader experience without using a screen reader;
- generate code and accessibility tests that do not remain aligned.

This template reduces those risks by treating accessibility as a behavioural and testable property of the generated design and code.

## Core outcomes

When used correctly, the template instructs the generating system to:

1. work within the configured JavaScript framework, UX design system, templates, brand system and repository conventions;
2. preserve approved fonts, colours, icons, layouts, tone of voice and interaction patterns wherever they can support an accessible outcome;
3. target WCAG 2.2 Level A and Level AA;
4. treat WCAG Level AAA as outside the required conformance scope;
5. use native HTML before creating custom ARIA widgets;
6. produce an accessible behaviour contract before or alongside implementation;
7. generate automated tests using axe and behavioural assertions;
8. generate manual tests that do not require a screen reader but inspect screen-reader-relevant foundations;
9. escalate tests that genuinely require a screen reader rather than guessing the result;
10. retain traceability between requirements, implementation, tests and evidence.

## What the template does not do

The template does not guarantee that generated output conforms to WCAG.

It is not:

- a replacement for accessibility specialists;
- a substitute for evaluation by disabled people;
- a complete accessibility audit;
- a substitute for testing complete pages and user journeys;
- proof that an interface works with every browser and assistive-technology combination;
- permission to describe a product as compliant because axe found no violations.

It creates a governed starting point, explicit expectations and a testable evidence structure.

## How design and accessibility are balanced

The template does not tell the model to replace an approved design system with generic accessible components.

When a UX design system exists, the system should:

- use its approved components and variants;
- retain its visual and interaction design;
- improve the underlying semantics and behaviour;
- reuse existing APIs and tokens;
- avoid creating competing local components;
- report any design-system defect that prevents an accessible result.

WCAG 2.2 A/AA defines the minimum accessibility outcome. Brand and design-system rules define how that outcome should be expressed.

If a brand or design-system decision cannot meet an applicable A/AA requirement, the model must not silently redesign the interface or falsely claim compliance. It must verify the conflict, try an implementation-only correction and identify the smallest design decision requiring review.

## Pattern hierarchy

When an approved UX design system exists, it is the primary source for component and visual decisions, subject to the WCAG 2.2 A/AA outcome.

When no design system exists, the template uses this order:

1. native HTML with the least custom behaviour necessary;
2. [Atomic Accessibility](https://www.atomica11y.com/) guidance;
3. [BBC GEL Technical Documentation](https://bbc.github.io/gel/) where Atomic Accessibility has a gap or lacks sufficient detail;
4. the relevant [WAI-ARIA Authoring Practices Guide pattern](https://www.w3.org/WAI/ARIA/apg/patterns/) when a custom widget is necessary;
5. a documented local pattern when the trusted sources do not address the problem.

Reference patterns guide the implementation. They do not import another organisation’s branding or automatically become production dependencies.

## Trusted sources

The template deliberately uses a limited source set to reduce contradictory or low-quality guidance.

| Source | Primary role |
|---|---|
| [W3C WCAG 2.2](https://www.w3.org/TR/WCAG22/) | Normative A/AA outcomes and conformance model |
| [WAI-ARIA APG patterns](https://www.w3.org/WAI/ARIA/apg/patterns/) | Expected behaviour for custom ARIA widgets |
| [WAI-ARIA APG: Read Me First](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/) | Native HTML preference and ARIA cautions |
| [BBC Mobile Accessibility Guidelines](https://www.bbc.co.uk/accessibility/forproducts/guides/mobile/) | Mobile and touch guidance |
| [BBC HTML Accessibility Guidelines](https://www.bbc.co.uk/accessibility/forproducts/guides/html/) | HTML implementation guidance |
| [BBC GEL Technical Documentation](https://bbc.github.io/gel/) | Framework-agnostic pattern implementation |
| [Atomic Accessibility](https://www.atomica11y.com/) | Default component guidance when no design system exists |
| [TetraLogical Screen Reader HTML Support](https://tetralogical.github.io/screen-reader-HTML-support/) | Browser, operating-system and screen-reader compatibility evidence |
| [axe-core rule descriptions](https://github.com/dequelabs/axe-core/blob/develop/doc/rule-descriptions.md) | Automated rule inventory and tags |

These sources do not all carry the same authority. WCAG defines the normative conformance outcome. The others provide implementation guidance, patterns, compatibility evidence or automated checks.

## Quick start

### 1. Copy the template

Add `Accessible_Generation_and_Testing_RAG_Template.md` to the project or knowledge base used by the AI system.

Keep an unchanged master copy if different products will create their own configured versions.

### 2. Complete the project configuration

Replace the `{{PLACEHOLDER_FIELDS}}` with project information, including:

- JavaScript framework and version;
- rendering and routing approach;
- UX design system and component catalogue;
- design tokens and interaction specifications;
- templates and application shell;
- brand, typography, colour and icon guidance;
- tone of voice and content rules;
- application and test repositories;
- test runner and pinned axe version;
- supported browser, device and operating-system matrix;
- high-risk or regulated user journeys;
- ownership and escalation routes.

An unknown field should remain visibly unknown until it can be resolved. Do not fill gaps with invented dependencies or conventions.

### 3. Add it to the AI context

Provide the configured document as a persistent instruction or RAG source for the design and development conversation.

The system should load it before generating interface designs, components, pages or test scripts.

### 4. Provide the project sources

Give the system access to the relevant:

- design-system documentation and source;
- brand documentation;
- templates;
- framework documentation;
- package manifest and lockfile;
- application repository;
- existing tests and test conventions;
- accessibility exception or defect register.

The template tells the system how to use these materials, but it cannot inspect information that has not been supplied or connected.

### 5. Request the artefact and its evidence together

For example:

> Create a date-picker component using the configured framework and design system. Include its accessible behaviour contract, implementation, automated accessibility tests, manual tests that do not require a screen reader, and any AT validation still required.

The template is designed to keep implementation and accessibility evidence together. Asking for code alone weakens that control.

## Expected output

For each generated artefact, the model should provide a proportionate version of:

1. scope and assumptions;
2. source and pattern decision;
3. accessible behaviour contract;
4. design or code implementation;
5. automated test script;
6. manual test script requiring no screen reader;
7. coverage and traceability matrix;
8. known limitations, assistive-technology escalation tests and residual risks.

The level of detail scales with the work. A button does not need a website-scale report, but it still needs its expected name, role, state, keyboard behaviour, visual states and relevant tests.

## Testing model

### Automated testing

The template requires more than a default axe scan. Depending on the artefact, generated automated tests should cover:

- stable and non-default UI states;
- expected roles and accessible names;
- keyboard interaction;
- focus movement and restoration;
- state and property changes;
- errors and status messages;
- loading, empty, disabled and success states;
- responsive and user-preference behaviour where automation is reliable.

The project’s installed axe version must be pinned and reported. WCAG 2.2 A/AA rules that are disabled by default may need to be enabled explicitly. AAA-only rules are excluded from the required gate. Axe best-practice rules should be run and reported separately from WCAG failures.

### Manual testing without a screen reader

The manual script covers areas that require human judgement or observation, including:

- keyboard-only operation;
- focus visibility and management;
- accessible names, roles, values and states in browser developer tools;
- heading, landmark, list and table structure;
- visible labels, instructions and error recovery;
- zoom, reflow and text spacing;
- colour and non-text contrast;
- forced colours and display preferences;
- reduced motion, timing and animation;
- pointer, touch and target behaviour;
- orientation, responsive layouts and content stress;
- complete page and process checks.

These checks examine foundations that affect screen-reader UX, but they do not prove what a screen reader announces or how efficiently a user can navigate the interface.

### Assistive-technology escalation

The template requires real assistive-technology testing when actual interoperability or spoken behaviour is a material risk. Examples include:

- custom ARIA composite widgets;
- live regions and asynchronous announcements;
- complex focus management;
- virtualised content;
- dialogs, comboboxes, grids, trees, menus and carousels;
- canvas or custom-rendered controls;
- unusual accessible-name computation;
- conflicting compatibility evidence;
- critical user journeys.

The model must specify the required screen reader, browser, operating system, task and expected user outcome. It must not fabricate a pass result.

## Resolving contradictions

Trusted sources can disagree because they address different contexts, were tested against different platform versions or represent different kinds of authority.

The template resolves a disagreement by:

1. defining the exact decision in dispute;
2. classifying each claim as a WCAG requirement, best practice, local rule or compatibility evidence;
3. checking whether the advice applies to the same pattern, state and platform;
4. checking the currency of the evidence;
5. applying the source hierarchy;
6. preferring native behaviour where it meets the need;
7. comparing viable variants through automated, manual and assistive-technology tests;
8. documenting the selected approach and residual risk.

Testing can show which approach is preferred for a defined user task and support matrix. It cannot prove that one implementation is universally optimal.

## Requirement classifications

The template keeps different obligations visible:

| Classification | Meaning |
|---|---|
| `WCAG-A-AA` | Directly supports an applicable WCAG 2.2 A or AA success criterion |
| `UX-BEST-PRACTICE` | Improves accessibility or usability beyond the stated conformance requirement |
| `DESIGN-SYSTEM-REQUIREMENT` | Approved local component, token or interaction rule |
| `BRAND-REQUIREMENT` | Approved visual, verbal or expressive brand rule |
| `FRAMEWORK-REQUIREMENT` | Necessary for correct technical implementation |
| `COMPATIBILITY-EVIDENCE` | Browser, device or assistive-technology support information |
| `RESEARCH-REQUIRED` | A material question cannot be resolved from available evidence |

This prevents useful guidance from being misrepresented as a WCAG obligation.

## Suggested repository structure

```text
/
├── README.md
├── Accessible_Generation_and_Testing_RAG_Template.md
├── configured/
│   └── Accessible_Generation_and_Testing_RAG_Project.md
├── decisions/
│   └── ADR-A11Y-001.md
├── evidence/
│   └── README.md
└── examples/
    └── example-component-output.md
```

Keep generated test files in the application’s established test structure rather than duplicating them in this documentation repository.

## Governance and maintenance

Review the configured RAG document when:

- WCAG guidance changes;
- the installed axe version changes;
- the JavaScript framework is upgraded;
- the UX design system or brand system changes;
- supported browsers, operating systems or devices change;
- new compatibility evidence affects an adopted technique;
- an accessibility defect reveals a gap in the generation rules;
- an exception reaches its review or expiry date.

Use the template’s source review log, adopted best-practice register and approved-exception register to preserve decision history.

An exception does not turn a WCAG failure into a pass. It records a known non-conformance, its user impact, ownership, compensating measure and expiry.

## Recommended ownership

The document works best when ownership is shared across:

- accessibility;
- design systems;
- brand and content;
- frontend engineering;
- quality assurance;
- product governance.

One named owner should remain accountable for versioning and review, while domain owners approve changes affecting their systems.

## Licence

Add the licence appropriate to the organisation and repository:

`{{LICENCE_NAME_AND_LINK}}`

Check the individual terms of referenced external sources before reproducing their examples. Linking to guidance does not transfer its licence to this project.

## Status

This README describes the initial reusable template. Configure and validate the template against a real project before treating it as an operational quality gate.
