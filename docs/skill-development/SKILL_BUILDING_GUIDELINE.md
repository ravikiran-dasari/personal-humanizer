# Skill-Building Guideline

This guideline applies the principles recorded in [Development references](./DEVELOPMENT_REFERENCES.md), especially the Agent Skills guidance on progressive disclosure, context efficiency and validation through real execution.

## Build in seven steps

1. **Define the boundary.** Write one sentence for the outcome, specific trigger phrases, required inputs, and explicit exclusions. Confirm that a skill is appropriate: use it for a repeatable on-demand workflow, not an always-on rule or a single parameterized prompt.
2. **Design the contract.** List invariants, allowed assumptions, blocking ambiguities, output shape, and success criteria before writing instructions.
3. **Create the minimum structure.** Add `.github/skills/<name>/SKILL.md`; make the frontmatter `name` match the folder and put discovery terms in `description`.
4. **Write the executable workflow.** Use ordered steps from intake through validation and delivery. Resolve conflicts with an explicit priority order when needed.
5. **Split only conditional detail.** Move long heuristics, profiles, examples, and fixtures into `references/`; put deterministic helpers in `scripts/`; put reusable output material in `assets/`. State when each resource should load.
6. **Test representative and adversarial cases.** Cover the normal path, protected data, ambiguity, already-correct input, conflicting guidance, unsupported requests, and output-format compliance.
7. **Validate and refine.** Fix discovery, broken links, unclear decisions, and failed invariants. Record uncertain guidance as provisional; do not turn one sample into a universal rule.

## Fast validation checklist

### Discovery and structure

- [ ] Skill is in a supported `<skills>/<name>/` location.
- [ ] `SKILL.md` exists and YAML frontmatter parses.
- [ ] `name` is 1-64 lowercase alphanumeric/hyphen characters and matches the folder.
- [ ] `description` is specific, trigger-rich, within 1024 characters, and includes key exclusions.
- [ ] Invocation fields are explicit or their defaults are intentional.

### Procedure and scope

- [ ] The body says what to do, in what order, and what “done” means.
- [ ] Required inputs, output contract, and blocking ambiguities are defined.
- [ ] Invariants and hard limits are separate from preferences.
- [ ] Conflict priority is explicit where instructions can compete.
- [ ] Out-of-scope work is named and routed appropriately.

### Resources and dependencies

- [ ] Every linked file exists at the exact relative path.
- [ ] All runtime dependencies needed for portability live in or are declared by the skill.
- [ ] Each reference has a clear loading condition.
- [ ] Scripts document runtime, arguments, outputs, and failure behavior.
- [ ] No resource duplicates core instructions without a reason.

### Evidence and examples

- [ ] Observations, recommendations, and uncertainties are labeled distinctly.
- [ ] Profiles identify evidence quality and do not overgeneralize limited samples.
- [ ] Examples include the decision rationale and protected invariants.
- [ ] Context-specific overlays do not silently become universal defaults.

### Evaluation

- [ ] Fixtures define request, input, invariants, expected behavior, and failures.
- [ ] Tests include normal, edge, ambiguity, no-change, and refusal/redirection cases as applicable.
- [ ] Outputs preserve protected facts, formats, and scope.
- [ ] Results record date, model, skill revision, pass/fail, and reviewer notes.
- [ ] A failed case leads to the smallest rule or example change that addresses the root cause.

## Release gate

A skill is ready when it is discoverable from realistic requests, can complete its main workflow without unstated knowledge, loads optional context only when relevant, has no broken dependencies, and passes its representative fixtures without violating invariants.

For this workspace specifically, release readiness also requires correcting the corpus filename references and deciding whether to bundle the corpus under `personal-humanizer/`.