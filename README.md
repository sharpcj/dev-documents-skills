# Development Document Skills

English | [中文](README.zh-CN.md)

A small collection of coding-agent skills for generating software engineering documents. The repository currently provides three document-type skills:

- High-Level Design documents (HLD)
- Single-feature technical design documents
- Requirement matrix and development schedule documents

Each skill triggers by document type first. After it is triggered, it determines the project type and chooses the right bundled template:

- `references/android-template.md` for Android projects
- `references/common-template.md` for non-Android software engineering projects

This avoids installing separate Android and common variants of the same skill, and leaves room for adding more domain templates later.

## Why this repository exists

Feature work often needs more than implementation code. Teams also need review-ready documents that describe scope, design choices, module boundaries, risks, interfaces, schedule, and verification plans. These skills turn repeated documentation work into reusable agent workflows.

The skills are written for practical engineering scenarios, including Android apps and system modules, backend services, Web frontends, iOS, desktop apps, cloud platforms, data platforms, AI/ML services, infrastructure, SDKs/libraries, CLI tools, and internal systems.

## Repository structure

```text
.
├── hld-generator/
│   ├── SKILL.md
│   └── references/
│       ├── android-template.md
│       └── common-template.md
├── technical-design-generator/
│   ├── SKILL.md
│   └── references/
│       ├── android-template.md
│       └── common-template.md
├── requirements-matrix-generator/
│   ├── SKILL.md
│   └── references/
│       ├── android-template.md
│       └── common-template.md
├── LICENSE
├── README.md
└── README.zh-CN.md
```

## Included skills

### `hld-generator`

Generates HLD documents based on PRDs, Jira or Confluence content, screenshots, existing design notes, API descriptions, architecture notes, or project code context.

Use it when the target output is a formal high-level design document, HLD, company/team HLD template, high-level system/module design, or design review checklist.

After triggering, the skill selects:

- Android template for Android apps, system apps, AOSP, APK/AAR, Android SDK/Framework, Android Gradle libraries, or Kotlin/Java Android modules.
- Common template for backend, Web, iOS, desktop, cloud, data, AI/ML, infrastructure, non-Android SDK/library, CLI, or internal system projects.

### `technical-design-generator`

Generates technical design documents for a single feature or version requirement.

Use it when the target output is a focused technical solution, implementation design, technical design, or feature-level review material.

The skill includes sections such as:

- Background
- Requirement description
- Technical solution
- Business flow diagram
- Data flow diagram
- Technical architecture topology
- Related module design
- Exception and boundary scenarios
- Risks and mitigation measures

### `requirements-matrix-generator`

Generates requirement matrix, development planning, workload estimation, and schedule documents for feature work.

Use it when the target output is task breakdown, effort estimate, development schedule, requirement matrix, work matrix, or Gantt chart.

The skill breaks work into reviewable and schedulable tasks, with guidance for:

- Reading original requirement and technical design materials first
- Splitting tasks into small development units
- Estimating work in person-days
- Preserving required columns and required quality rows
- Handling dependencies and risk items
- Generating Mermaid Gantt charts for multi-person schedules

## Project type selection

The skills do not trigger separately for Android and non-Android projects. Instead, each skill asks or infers the project type after triggering.

Use the Android template when the context clearly mentions Android-specific signals such as:

- Android App, AOSP, system app, APK, AAR
- Gradle Android Library, AndroidManifest, minSdk, targetSdk
- Android SDK, Android Framework, AIDL, Intent, Broadcast, ContentProvider
- Kotlin/Java Android, Activity, Fragment, ViewModel, Service, Receiver, Provider, Worker, Compose/XML

Use the common template when the context clearly belongs to non-Android software engineering, such as:

- Backend service, Web frontend, iOS, desktop, cloud platform
- Data platform, AI/ML service, infrastructure, middle platform
- Non-Android SDK/library, CLI, internal enterprise system
- API gateway, database, cache, message queue, object storage, CI/CD, deployment, observability

If the user only says “App”, “client”, “mobile”, “SDK”, “framework”, “design document”, or “template” without enough project context, the skill should ask a clarifying question before choosing a template.

## How to use

Copy or import the skill directories you need into your coding agent's skill, rule, or instruction directory. The exact target path depends on the agent you use. For example:

```bash
cp -R hld-generator /path/to/your-agent/skills/
cp -R technical-design-generator /path/to/your-agent/skills/
cp -R requirements-matrix-generator /path/to/your-agent/skills/
```

Then restart or reload your coding agent if it does not pick up new skills automatically.

Example prompts:

```text
Use the HLD generator to create a high-level design document based on this PRD and the existing module design.
```

```text
Generate a feature technical design document from this requirement description and code path.
```

```text
Based on this PRD and technical design, create a requirement matrix. Start date is 2026-07-01 and there are 3 developers.
```

## Input expectations

The skills work best when you provide concrete source material, such as:

- PRD, Jira, Confluence, ERGO/GD, or other requirement content
- Existing technical design, HLD, architecture notes, or interface documents
- Project paths, modules, package names, services, classes, APIs, or call chains
- Interface definitions, protocol fields, screenshots, interaction flows, deployment notes, or logs
- Schedule constraints, start date, end date, and developer count for requirement matrices

When key information is missing, the skills are designed to mark items as "to be confirmed" instead of inventing details.

## Design principles

- Trigger by document type first, then select the project template.
- Ask for project type when the context is ambiguous.
- Read the source material before writing the document.
- Keep required template sections and review checklists intact.
- Use domain-specific engineering context after choosing the template.
- Preserve uncertainty explicitly with "to be confirmed" markers.
- Produce Markdown documents that can be reviewed and iterated by engineering teams.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
