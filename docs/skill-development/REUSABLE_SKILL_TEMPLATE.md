# Reusable Agent Skill Template

Use this as a starting structure, then remove every optional section that does not earn its context cost.

## Standard layout

```text
.github/skills/<skill-name>/
|-- SKILL.md                  # Mandatory
|-- references/              # Optional: detailed guidance loaded on demand
|   |-- decision-guide.md
|   |-- examples.md
|   `-- validation-cases.md
|-- scripts/                 # Optional: executable, deterministic helpers
`-- assets/                  # Optional: templates or boilerplate used in outputs
```

Keep dependencies inside the skill directory when portability matters. Reference resources directly from `SKILL.md` and prefer one-level-deep links.

## Mandatory `SKILL.md` skeleton

```markdown
---
name: <lowercase-hyphenated-name>
description: '<Capability>. Use when <specific triggers and tasks>. Do not use for <important exclusions>.'
---

# <Human-readable skill title>

<One or two sentences stating the outcome and core constraint.>

## When to use

- <Trigger or use case>
- <Trigger or use case>

## Workflow

1. <Determine inputs, scope, and output contract.>
2. <Protect invariants or capture the baseline.>
3. <Perform the domain procedure.>
4. <Validate against explicit success criteria.>
5. <Return or write the result in the required format.>

## Constraints

- <Non-negotiable accuracy, safety, or compatibility rule.>
- <Scope boundary or prohibited action.>

## Resources

- [Decision guide](./references/decision-guide.md): read when <condition>.
- [Examples](./references/examples.md): read when <condition>.
- [Validation cases](./references/validation-cases.md): use only when evaluating the skill.
```

## Optional frontmatter

```yaml
argument-hint: '<input or parameter hint>'
user-invocable: true
disable-model-invocation: false
```

Use `user-invocable: false` to hide the slash command while retaining automatic loading. Use `disable-model-invocation: true` to require explicit invocation. Omit either field only when its platform default is intentional.

## Optional reference templates

### Decision guide

```markdown
# Decision guide

## <Decision or pattern>

**Purpose:** <Why this matters>  
**Actionability:** <Whether it justifies action by itself>

<Rule and procedure.>

Preserve or skip this action when:

- <Exception>
- <Exception>
```

### Evidence-based profile

```markdown
# <Context> profile

## Evidence status

<State whether guidance is observed, inferred, or provisional.>

- **Direct preference:** <Explicitly stated choice>
- **Observed pattern:** <Recurring pattern and source IDs>
- **Working hypothesis:** <Limited or mixed evidence>
- **Provisional default:** <Fallback with no personal evidence>

## Guidance

- **Evidence: <label>.** <Instruction>

## Update rule

Upgrade or remove guidance only after <minimum representative evidence>.
```

### Example

```markdown
## <Decision illustrated>

**Input:**

> <Original>

**Output:**

> <Result>

**Why:** <Principle applied, invariant preserved, and tradeoff resolved.>
```

### Validation case

```markdown
## <Case number and behavior>

**Request:** <Exact request>

**Input:**

> <Fixture>

**Must preserve:** <Invariants>

**Expected:** <Acceptable behavior, not one mandatory wording>

**Unacceptable:** <Concrete failure conditions>
```

## Mandatory versus skill-specific choices

| Element | Mandatory | Use when |
|---|---:|---|
| Supported skill directory | Yes | Always |
| `SKILL.md` | Yes | Always |
| Matching `name` and folder | Yes | Always |
| Discovery-oriented `description` | Yes | Always |
| Procedural body | Functionally yes | Always |
| Exact headings shown above | No | They improve navigation for multi-step skills |
| Priority hierarchy | No | Instructions may conflict |
| Output modes | No | The task has multiple return contracts |
| Hard limits | No | Accuracy, safety, or compliance rules override preferences |
| References | No | Details are conditional or would make `SKILL.md` monolithic |
| Scripts | No | A deterministic operation can be automated and validated |
| Assets | No | The skill produces standardized artifacts |
| Examples | No | Rules involve judgment or exceptions |
| Validation fixtures | No | Behavior needs regression evaluation |
| Profiles/sample corpora | No | Output adapts to a user, audience, platform, or domain |

## Formatting and design rules

- Put trigger language in `description`; discovery cannot depend on body text alone.
- Keep `SKILL.md` focused and below the platform reference's 500-line recommendation.
- State procedures as ordered actions and validation as observable pass/fail conditions.
- Separate non-negotiable constraints from defaults and preferences.
- Give each optional resource a loading condition; avoid “read everything” instructions.
- Use relative `./` links and verify every target, including filename case and location.
- Label recommendations, inferences, and provisional guidance instead of presenting them as observations.
- Make examples teach a decision rule; do not use them merely to add volume.
- Keep evaluation fixtures independent of one exact output unless exact output is the contract.
- Avoid external dependencies unless a script genuinely needs them; declare and document any that are added.