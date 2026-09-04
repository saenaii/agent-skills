---
name: legacy-project-profiler
description: Build a high-level mental model of a legacy or unfamiliar codebase from its project tree, dependencies, and entry files. Use for onboarding, architecture understanding, or system audits; avoid line-by-line code review.
---

# Legacy Project Profiler

Help software engineers understand a legacy or unfamiliar project quickly, using plain, business-oriented English.

Focus on the system's purpose, its major components, primary data flows, and the best starting points for further investigation. Avoid low-level implementation details, utility functions, and line-by-line explanations.

## When to Use

Use this skill when a user provides any of the following and asks to onboard to, understand, map, or audit a codebase:

- A repository path or codebase directory tree
- Dependency manifests such as `go.mod`, `package.json`, `Cargo.toml`, or `pom.xml`
- Core entry files, API schemas, or configuration files

## Information to Inspect

Gather the smallest set of evidence needed to form a reliable architectural view:

1. Project directory tree, preferably to depth 3-4
2. Dependency manifests
3. Entry points and API schemas when available
4. Configuration files and infrastructure integration points when relevant

If the available evidence is insufficient to identify a primary execution path, state the uncertainty and name the most useful additional file or directory to inspect.

## Output

Write in English and produce both:

1. A written codebase profile using the sections below, returned directly in the conversation.
2. A standalone, interactive HTML architecture map at `output/<project-name>-architecture.html`, where `output/` sits alongside this `SKILL.md`. Tell the user where to open the file locally.

### 1. Executive Summary

Explain:

- **Core Purpose:** What the project does from a business perspective.
- **System Role:** Its likely role in the wider ecosystem, such as an API service, background worker, integration service, internal tool, or user-facing application.

Clearly distinguish confirmed findings from reasonable inferences.

### 2. Core Architecture & Key Modules

Group the codebase into these functional layers:

- **API / Entry Layer:** How work enters the system—HTTP, gRPC, CLI, scheduled jobs, message consumers—and the relevant folders.
- **Core Logic Layer:** The directories or packages responsible for business rules and orchestration.
- **Data & Infrastructure Layer:** Databases, caches, queues, external APIs, filesystems, or other integrations, along with where they appear in the codebase.

Do not force a layer when the project structure does not support it. Explain the project's actual organization instead.

### 3. Visual Architecture Map

Create `output/<project-name>-architecture.html` as a self-contained HTML file. Use inline CSS and JavaScript only; do not depend on a build step, local server, CDN, or external assets. Do not write visual artifacts into the analyzed codebase.

Show three clearly separated visual regions, arranged as follows:

- **API Layer:** top-left region
- **Core Logic Layer:** middle region
- **Data & Infra Layer:** bottom-right region

Place component cards inside their appropriate region. Each card should use a concise label containing its responsibility and, when useful, its folder or package. Include only the components needed to explain the primary architecture.

Connect related components with directional arrows. Add a short label when it clarifies the relationship, such as `gRPC request`, `reads/writes`, `publishes task`, or `queries`.

Make the HTML usable without reading the written profile. Provide exactly three visual tabs:

1. **High-Level Data Flow:** a directed acyclic graph (DAG) for the primary business scenario. It must show how a request enters the system, the core decision or orchestration steps, data writes or reads, asynchronous handoffs, and resulting consumers or outputs. Use the API, Core Logic, and Data & Infra layers as visually distinct regions.
2. **API Flows:** an API-specific execution-path DAG.
3. **Codebase Profile:** the complete written codebase profile, using the same Executive Summary, Core Architecture & Key Modules, Core APIs, Primary Data Flow, Key Files to Watch, and Getting Started Checklist content returned in the conversation.

- Lay out both DAGs in compact tiers or branches, not as one long horizontal sequence. Use responsive SVG or an equivalent scalable layout so the map fits its container without horizontal overflow, clipped nodes, or overlapping labels.
- Select 3-5 core APIs from the project's actual public API contract. Prioritize APIs that represent the main write path, main read path, important asynchronous work, and other high-value business operations.
- In the **API Flows** tab, display the selected APIs as selectable controls. Select the first API by default.
- When the user selects an API, replace the flow map and detail panel with that API's real directed acyclic graph, traced from its API definition through the relevant handler, core services, storage clients, external integrations, queues, and asynchronous consumers when applicable.
- Use concise component cards and labelled directional arrows. Each card must identify the real directory, package, or file that implements that step.
- Clearly distinguish synchronous request handling from asynchronous work, such as a queue handoff and later consumer processing.
- Do not use a generic `Handler -> Service -> Database` diagram when the code shows a more specific path. Do not invent missing steps; state an uncertainty in the detail panel if the implementation cannot be confirmed.
- Keep pan, zoom, and reset-to-fit controls available in both tabs.
- Keep component cards selectable. Selecting a card should highlight its connected arrows and show its role, relevant folders/files, direct dependencies, and its position in the selected API flow.
- Include a small legend that distinguishes the three architecture layers, synchronous arrows, and asynchronous arrows.
- Keep the layout readable at a normal browser width. Nodes, labels, arrows, and regions must not overlap or require horizontal scrolling.

In the written profile, add a **Core APIs** subsection after the architecture summary. List the same 3-5 APIs, their business purpose, and the implementation entry file used to build each visual flow.

After creating the file, open it or inspect its rendered output when available. Verify that it works without network access, all three tabs can be selected, every chosen API switches to its own flow, the Codebase Profile matches the text returned in the conversation, and each component card can be selected.

### 4. Primary Data Flow

Choose one representative and well-supported business scenario, such as creating an order, processing a message, or retrieving a profile.

Show its high-level path in a compact form, for example:

`Router/Handler -> Service/Domain -> Repository/DAO -> Database`

Then map each step to its relevant directory, package, or file. Do not speculate about internal behavior that the supplied evidence does not establish.

### 5. Key Files to Watch

List 3-5 files with the highest onboarding value, such as:

- Application entry point
- Route, handler, or API schema definition
- Core service or domain interface
- Configuration bootstrap
- Database, queue, or external-client wiring

For each, explain in one sentence why it is a useful starting point.

### 6. Getting Started Checklist

Provide exactly three concrete next steps:

1. **Data Model:** The first entity, schema, table, or struct to inspect.
2. **Execution Path:** The first endpoint, command, consumer, or focused test to run or debug.
3. **Environment:** The configuration file, deployment manifest, or environment variables to examine.

Make recommendations specific to the inspected project. If a detail cannot be established, say what to inspect next rather than inventing it.

