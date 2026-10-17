# Agent Skills

A small collection of reusable skills for Codex. Each skill gives the agent focused instructions for a specific kind of work, such as writing code, explaining an unfamiliar project, or simplifying complex content.

## Available Skills

| Skill | Purpose |
| --- | --- |
| [`coding`](skills/coding/SKILL.md) | Provides a disciplined workflow for repository, language, and code changes. Includes Go guidance and self-validation notes. |
| [`content-simplifier`](skills/content-simplifier/SKILL.md) | Simplifies complex documents and rewrites drafts so beginners can understand them without losing accuracy. |
| [`legacy-project-profiler`](skills/project-profiler/SKILL.md) | Builds a high-level mental model of an unfamiliar or legacy codebase and can generate an interactive architecture map. |

## Repository Layout

```text
.
├── README.md
└── skills/
    ├── coding/
    │   ├── SKILL.md
    │   └── reference/
    │       └── golang/
    ├── content-simplifier/
    │   ├── SKILL.md
    │   └── agents/
    │       └── openai.yaml
    └── project-profiler/
        └── SKILL.md
```

Every skill has a required `SKILL.md` file. A skill may also include supporting references, scripts, assets, or UI metadata when those files provide real value.

## Using a Skill

Skills are designed to be discovered automatically from their name and description. You can also invoke one explicitly when supported by your Codex environment.

Examples:

- Use `coding` when implementing or refactoring repository code.
- Use `content-simplifier` when summarizing a complex document or rewriting a draft for clarity.
- Use `legacy-project-profiler` when onboarding to an unfamiliar codebase or creating an architecture overview.

## Creating a New Skill

1. Create a directory under `skills/` using a lowercase, hyphenated name.
2. Add a `SKILL.md` with YAML frontmatter containing `name` and `description`.
3. Keep the description specific about what the skill does and when it applies.
4. Put the essential workflow in `SKILL.md`; move substantial, conditional guidance into `references/`.
5. Add scripts or assets only when they directly support repeatable work.
6. Validate the skill with the Codex skill creator validator before publishing it.

Minimal example:

```markdown
---
name: example-skill
description: Do one focused task when the user asks for that task.
---

# Example Skill

Describe the outcome, important constraints, and the workflow needed to produce it.
```

## Design Principles

- Keep each skill focused on one recognizable capability.
- Preserve the user's intent and authorization boundaries.
- Prefer concise, actionable instructions over generic advice.
- Disclose detail progressively so unrelated resources are not loaded unnecessarily.
- State uncertainty instead of inventing missing facts.
- Validate observable behavior when a skill creates files or other artifacts.

## Contributing

Keep changes focused on the affected skill. Before opening a change, inspect the skill's existing instructions, validate its structure, and run `git diff --check` for documentation changes.
