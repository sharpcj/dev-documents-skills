# Android Dev Documents Skills

English | [中文](README.zh-CN.md)

A small collection of coding-agent skills for generating Android development documents. The repository currently focuses on three recurring documentation tasks in Android app and system feature work:

- High-Level Design documents (HLD)
- Single-feature technical design documents
- Requirement matrix and development schedule documents

Each skill includes a `SKILL.md` instruction file and, where needed, a reusable Markdown template under `references/`.

## Why this repository exists

Android feature work often needs more than implementation code. Teams also need review-ready documents that describe scope, design choices, module boundaries, risks, interfaces, schedule, and verification plans. These skills turn that repeated documentation work into reusable agent workflows.

The skills are written for practical Android engineering scenarios, including app features, system apps, SDK or framework capabilities, cross-module integrations, device adaptation, non-functional requirements, and release planning.

## Repository structure

```text
.
├── hld-generator/
│   ├── SKILL.md
│   └── references/
│       └── template.md
├── technical-design-generator/
│   ├── SKILL.md
│   └── references/
│       └── template.md
├── requirements-matrix-generator/
│   ├── SKILL.md
│   └── references/
│       └── template.md
├── LICENSE
├── README.md
└── README.zh-CN.md
```

## Included skills

### `hld-generator`

Generates Android-oriented HLD documents based on PRDs, ERGO/GD materials, Jira or Confluence content, screenshots, existing design notes, API descriptions, or Android project context.

The skill keeps the company-style HLD template structure intact, including:

- Document history
- Introduction and reference material
- Requirement analysis
- Overall architecture design
- Module-level design
- Interface design
- Non-functional design
- Concurrency, data structure, physical resource, and error handling sections
- A complete 20-item HLD review checklist

Use it when the target output is a formal high-level design document.

### `technical-design-generator`

Generates technical design documents for a single Android feature or version requirement.

The skill is designed for feature-level review materials and includes sections such as:

- Background
- Requirement description
- Technical solution
- Business flow diagram
- Data flow diagram
- Technical architecture topology
- Related module design
- Exception and boundary scenarios
- Risks and mitigation measures

Use it when the target output is a focused technical solution for one Android feature.

### `requirements-matrix-generator`

Generates requirement matrix, development planning, workload estimation, and schedule documents for Android feature work.

The skill breaks work into reviewable and schedulable tasks, with guidance for:

- Reading original requirement and technical design materials first
- Splitting tasks into small Android development units
- Estimating work in person-days
- Preserving required columns and required quality rows
- Handling dependencies and risk items
- Generating Mermaid Gantt charts for multi-person schedules

Use it when the target output is a task matrix, effort estimate, or development schedule.

## How to use

Copy or import the skill directories you need into your coding agent's skill, rule, or instruction directory. The exact target path depends on the agent you use. For example:

```bash
cp -R hld-generator /path/to/your-agent/skills/
cp -R technical-design-generator /path/to/your-agent/skills/
cp -R requirements-matrix-generator /path/to/your-agent/skills/
```

Then restart or reload your coding agent if it does not pick up new skills automatically.

After installation, ask your coding agent to generate the corresponding document with enough context. Example prompts:

```text
Use the HLD generator to create an Android high-level design document based on this PRD and the existing module design.
```

```text
Generate an Android feature technical design document from this requirement description and code path.
```

```text
Based on this PRD and technical design, create a requirement matrix. Start date is 2026-07-01 and there are 3 Android developers.
```

## Input expectations

The skills work best when you provide concrete source material, such as:

- PRD, ERGO, GD, Jira, Confluence, or other requirement content
- Existing technical design or architecture notes
- Android project paths, modules, package names, classes, APIs, or call chains
- Interface definitions, protocol fields, screenshots, or interaction flows
- Schedule constraints, start date, end date, and developer count for requirement matrices

When key information is missing, the skills are designed to mark items as "to be confirmed" instead of inventing details.

## Design principles

- Read the source material before writing the document.
- Keep required template sections and review checklists intact.
- Prefer Android-specific implementation context over generic descriptions.
- Preserve uncertainty explicitly with "to be confirmed" markers.
- Cover lifecycle, permissions, compatibility, reliability, security, testing, and rollback concerns where relevant.
- Produce Markdown documents that can be reviewed and iterated by engineering teams.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
