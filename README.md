# Personal Humanizer

A personal Agent Skill for rewriting prose in a natural, direct voice while preserving meaning, factual details, and the writer's intent.

## Repository layout

```text
.
|-- .github/
|   `-- skills/
|       `-- personal-humanizer/
|           |-- SKILL.md
|           `-- references/
|-- docs/
|   |-- skill-analysis/
|   `-- skill-development/
|-- my_personal_socialmedia_posts_examples.txt
|-- .gitignore
|-- CONTRIBUTING.md
`-- README.md
```

The skill is in `.github/skills/personal-humanizer/`. Its `SKILL.md` contains the core workflow; supporting guidance and evaluation cases live in `references/`. The `docs/` directory contains the design analysis and maintenance guidance. The annotated social-post corpus is source material for the LinkedIn style profile, not a dependency that must be loaded for every rewrite.

## Use the skill

Use the supported Agent Skills workflow in your compatible editor or agent. The skill's discovery metadata and instructions are in `.github/skills/personal-humanizer/SKILL.md`; no build or package installation is currently required.

## Maintain the skill

Before changing the skill, review [the skill-building guideline](docs/skill-development/SKILL_BUILDING_GUIDELINE.md) and [the analysis](docs/skill-analysis/SKILL_ANALYSIS.md). Validate frontmatter, folder/name agreement, relative links, and representative cases in `references/validation-cases.md` after edits. The cases are currently evaluated manually; there is no automated test runner or CI workflow in this repository.

## Before publishing

This repository includes an MIT license. Review the annotated writing samples for personal information and confirm that you have permission to publish them.