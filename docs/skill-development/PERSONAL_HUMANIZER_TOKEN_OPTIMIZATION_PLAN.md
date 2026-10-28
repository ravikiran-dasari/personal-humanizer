# Personal Humanizer Token Optimization Plan

## 1. Purpose and scope

This document plans a token-reduction experiment for `.github/skills/personal-humanizer/`. It records the current baseline, likely sources of unnecessary token use, proposed changes, evaluation method, and accept/reject rules.

This is a planning artifact only. Do not modify the current skill until the plan is reviewed and approved. When implementation starts, preserve the current files as the baseline and create a separate candidate version for comparison.

## 2. Measurement method

### Tokenizer and date

- Audit date: 2026-10-28
- Tokenizer package: `tiktoken 0.14.0`
- Primary encoding: `o200k_base`
- Cross-check encoding: `cl100k_base`
- Counted content: complete UTF-8 file contents, including YAML frontmatter and Markdown syntax

Token counts vary by model and provider. Use these figures as a reproducible engineering baseline, not as an exact billing forecast for every runtime.

### Reproduction command

Use one tokenizer and package version for both baseline and candidate measurements. Record upgrades rather than silently changing the measurement method.

```python
from pathlib import Path
import tiktoken

root = Path(".github/skills/personal-humanizer")
encoding = tiktoken.get_encoding("o200k_base")
files = [root / "SKILL.md", *sorted((root / "references").glob("*.md"))]

for path in files:
    text = path.read_text(encoding="utf-8")
    print(path.as_posix(), len(encoding.encode(text)))
```

## 3. Current audit baseline

### File-level measurements

| File | Lines | Words | `cl100k_base` | `o200k_base` | Expected loading |
|---|---:|---:|---:|---:|---|
| `SKILL.md` | 105 | 1,300 | 1,692 | 1,683 | Every activated use |
| `references/personal-style-profile.md` | 54 | 614 | 757 | 752 | Most rewrites without stronger guidance |
| `references/linkedin-style-profile.md` | 91 | 929 | 1,177 | 1,181 | Professional social posts |
| `references/output-modes.md` | 66 | 380 | 487 | 487 | Only when response contract is unclear |
| `references/pattern-catalog.md` | 154 | 1,355 | 1,845 | 1,833 | Only for uncertain pattern diagnosis |
| `references/examples.md` | 269 | 1,317 | 1,600 | 1,589 | Only for unresolved rules or exceptions |
| `references/validation-cases.md` | 233 | 1,344 | 1,883 | 1,871 | Evaluation only |
| **Total** | **972** | **7,239** | **9,441** | **9,396** | Not normally loaded together |

The total bundle size is not the main runtime cost because references load on demand. The important measurements are the paths below.

### Representative runtime paths

| Runtime path | `o200k_base` tokens | Notes |
|---|---:|---|
| Discovery metadata only | 95 | Always-loaded `name` and `description` content |
| Activated core body only | 1,587 | `SKILL.md` body after activation |
| Ordinary rewrite with default profile | 2,434 | Most likely common path |
| LinkedIn rewrite with both profiles | 3,614 | Common specialized path |
| Rewrite with unclear output mode | 2,920 | Core, personal profile, and output modes |
| Rewrite requiring pattern diagnosis | 4,266 | Core, personal profile, and pattern catalog |

### Existing strengths to retain

- The description clearly states what the skill does, when to use it, and when not to use it.
- The skill already uses one-level reference links and progressive disclosure.
- Examples and validation fixtures are outside the activated core.
- Evaluation-only content is explicitly excluded from ordinary rewrites.
- The workflow protects facts, uncertainty, technical content, quotations, URLs, and user voice.
- Pattern guidance avoids unreliable AI-authorship and detector claims.

## 4. Audit findings

### A. Repeated activated instructions

The same fidelity requirements appear in several places in `SKILL.md`:

- `Priorities` protects meaning, facts, names, numbers, dates, citations, and technical accuracy.
- Workflow steps 3 and 6 repeat protected-detail collection and verification.
- `Editing gotchas` repeats unsupported-addition and source-claim rules.
- `Hard limits` restates invention, claim strength, detector, regional-language, and protected-literal constraints.

These repetitions reinforce important behavior, so they should be consolidated into one prominent invariant block rather than deleted independently.

### B. Output-mode duplication

`SKILL.md` contains four useful mode summaries, then links to `output-modes.md` in the mode section and again in `Resources`. The summaries are sufficient for most requests. Keep them in the core, but reduce repeated navigation wording and load the reference only for genuine ambiguity.

### C. Pattern-catalog duplication

The catalog is linked from the workflow, repeated after `Editing gotchas`, and listed again under `Resources`. Use one conditional instruction in the workflow and one compact resource index entry.

### D. Overlap between generic style and personal profile

The core defaults and personal profile both instruct the agent to use direct, natural, plain, lightly conversational language; preserve useful personality and repetition; avoid forced variation; and respect regional English. This makes the common path pay twice for similar advice.

Keep universal editing behavior in `SKILL.md`. Keep only genuinely personal defaults and evidence status in the personal profile.

### E. LinkedIn profile verbosity

The LinkedIn profile repeats evidence labels, professional/curious/practical tone, technical precision, and formatting cautions across `Voice`, `Preferred defaults`, `Formatting and engagement`, and `Preserve the voice, correct the noise`.

Retain evidence provenance and the user's confirmed length preference. Consolidate repeated tendencies, and keep post-type structures only if evaluation shows they materially improve results.

### F. Low-frequency content is already mostly well placed

The pattern catalog, examples, and validation cases are large but dormant. Their raw size does not affect ordinary runtime unless the agent reads them. Do not shorten them merely to improve the bundle-total metric. Optimize their routing language and only shorten content that is repeatedly loaded or demonstrably unused.

### G. Rarely needed or weakly justified content

Review these items during the candidate refactor:

- Generic explanations the model already understands, such as why emails differ from legal writing.
- Multiple examples proving the same preservation rule.
- Numeric LinkedIn defaults based only on mixed-sample hypotheses, especially emoji, paragraph, and bullet counts.
- Development-source commentary in the pattern catalog during runtime. It may remain as provenance if it is never loaded for ordinary tasks.
- Calibration-input lists that are useful for profile maintenance but not normal rewriting. Consider a maintenance-only reference if they are frequently loaded with the default profile.

## 5. Refactor proposal

Apply changes in small stages. Measure and evaluate after each stage so a regression can be traced to one decision.

### Stage 0: Freeze the baseline

1. Record the current commit hash or archive an exact copy outside the candidate directory.
2. Record model name/version, runtime, system instructions, temperature or reasoning settings, and tokenizer version.
3. Save baseline outputs for all 15 existing validation cases.
4. Do not edit baseline outputs after seeing candidate results.

### Stage 1: Consolidate `SKILL.md`

1. Keep the current YAML discovery meaning. Shorten the description only if trigger coverage remains unchanged.
2. Replace repeated fidelity language with one early `Non-negotiable invariants` block covering:
   - preserve meaning, facts, scope, certainty, commitments, citations, and technical details;
   - never invent content;
   - preserve protected literals unless explicitly authorized;
   - never claim authorship or detector evasion from style.
3. Keep one compact priority order.
4. Reduce the workflow to five steps: classify, select voice guidance, protect details, rewrite, validate/return.
5. Merge `Editing gotchas`, `Default style preferences`, and `Match the kind of writing` into compact decision rules.
6. Keep the four output-mode summaries in the core because they directly control behavior.
7. Keep one conditional link per reference and one compact reference index.
8. Remove explanatory prose that does not change a decision.

Initial target: reduce complete `SKILL.md` from 1,683 to 1,050-1,200 `o200k_base` tokens.

### Stage 2: Tighten the default personal profile

1. Keep the provisional evidence warning in two or three lines.
2. Keep only distinctive personal defaults: plain professional Indian English, direct and practical tone, mostly short or medium sentences, cautious use of contractions, and preservation of clear regional wording.
3. Remove advice already guaranteed by the core skill, including factual fidelity, generic clarity, and prohibition on fabricated errors.
4. Move profile-maintenance and sample-calibration guidance to a separate maintenance reference if it is not needed during ordinary rewriting.
5. Retain the direct LinkedIn routing link.

Initial target: reduce the profile from 752 to 350-450 `o200k_base` tokens.

### Stage 3: Tighten the LinkedIn profile

1. Consolidate repeated evidence-status passages into one short provenance section.
2. Combine repeated tone and technical-language rules.
3. Separate confirmed preferences from experimental defaults.
4. Keep the preferred 180-300 word range because it has direct evidence.
5. Treat emoji, paragraph, bullet, hashtag, and closing-question counts as optional starting points, or remove them if tests show no benefit.
6. Replace three long post-type workflows with a compact conditional matrix if equivalent quality is maintained.
7. Remove rules already enforced by `SKILL.md` or the general profile.

Initial target: reduce the LinkedIn profile from 1,181 to 650-800 `o200k_base` tokens.

### Stage 4: Review optional references without forcing reductions

1. Keep `validation-cases.md` unchanged during the first comparison to prevent evaluation leakage.
2. Keep `examples.md` on demand. Remove an example later only when another example tests the same rule and no evaluation depends on the distinction.
3. Keep the pattern catalog's decision categories and exceptions. Consider shortening repeated explanations only after core-path changes pass.
4. Keep output-mode details on demand. Remove templates only if the mode summaries produce the same contract compliance.
5. Add a short table of contents to references over 100 lines only if the target runtime previews partial files or navigation tests show missed sections.

### Stage 5: Improve routing precision

Use explicit conditions in the candidate `SKILL.md`:

| Reference | Load condition | Do not load when |
|---|---|---|
| Personal style profile | No stronger sample or house style is available | The user supplies representative voice guidance |
| LinkedIn style profile | LinkedIn or professional social post | Email, report, internal message, or technical document |
| Output modes | Response contract remains unclear after mode summaries | Mode is obvious from the request |
| Pattern catalog | A suspected pattern or exception is genuinely unclear | Routine naturalness edit |
| Examples | A rule remains ambiguous after applicable instructions | The decision is already clear |
| Validation cases | Evaluating or changing the skill | Any ordinary rewrite |

## 6. Evaluation design

### Identical-run controls

For every baseline/candidate pair:

1. Use a fresh session or isolated context.
2. Use the same model and version.
3. Use identical system/developer instructions and tool availability.
4. Use the exact same request, source text, attachments, and voice sample.
5. Use the same generation settings where configurable.
6. Run each case at least three times if sampling is nondeterministic.
7. Randomize or blind output labels during human review.
8. Record which references the agent actually reads.

### Phase A: Cheap discriminating smoke test

Run these cases immediately after the first candidate edit:

- Case 2: protected command, environment variable, status code, and URL
- Case 8: dates, commitment, scope, citation marker, and link
- Case 10: detector-evasion request
- Case 14: default personal style profile

Reject or repair the candidate before wider testing if any hard invariant fails.

### Phase B: Full existing suite

Run all 15 cases in `references/validation-cases.md` against baseline and candidate. Score each output on:

| Dimension | Scoring rule |
|---|---|
| Correctness | All source facts and relationships preserved |
| Completeness | No required detail, limitation, or instruction omitted |
| Instruction compliance | Output mode, house style, voice hierarchy, and hard limits followed |
| Naturalness and voice | Blind reviewer preference on a 1-5 scale |
| Token usage | Input context, references loaded, output tokens, and total tokens recorded |

Hard-invariant failures are binary and override average scores.

### Phase C: Routing tests

Add focused tests that verify loading behavior, not only final prose:

1. Ordinary email with no voice sample: load core plus personal profile only.
2. Email with a strong voice sample: do not load the personal profile unless needed to resolve a conflict.
3. LinkedIn post: load core, personal profile, and LinkedIn profile.
4. Already-natural text: avoid catalog and examples; make no unnecessary rewrite.
5. Ambiguous pattern exception: load the pattern catalog, but not examples unless still unresolved.
6. Skill-maintenance request: load validation cases; ordinary rewriting must not load them.

### Phase D: Real-work samples

Use at least five anonymized examples representative of actual use:

- short professional email;
- internal project update;
- technical explanation;
- LinkedIn post;
- already-natural text needing minimal change.

These should not duplicate the validation fixtures. Reviewers should compare baseline and candidate outputs without knowing which is which.

## 7. Token metrics and targets

Record both static and observed runtime metrics.

### Static metrics

- YAML metadata tokens
- `SKILL.md` tokens
- each reference file's tokens
- common-path totals
- percentage change from baseline

Use:

$$
\text{Reduction \%} = \frac{\text{Baseline tokens} - \text{Candidate tokens}}{\text{Baseline tokens}} \times 100
$$

### Observed runtime metrics

- instructions loaded before the task;
- references read and tokens added by each;
- prompt/input tokens reported by the runtime;
- completion/output tokens;
- total tokens per case;
- median and worst-case totals across repeated runs.

### Initial targets

| Path | Baseline | Candidate target | Minimum reduction goal |
|---|---:|---:|---:|
| Discovery metadata | 95 | At or below baseline | No trigger regression |
| `SKILL.md` complete | 1,683 | 1,050-1,200 | About 29-38% |
| Ordinary default path | 2,434 | 1,400-1,650 | About 32-42% |
| LinkedIn path | 3,614 | 2,050-2,400 | About 34-43% |

Targets are hypotheses, not acceptance criteria by themselves. Quality gates take priority over token reduction.

## 8. Acceptance and rejection rules

### Accept a change only when all conditions pass

- Zero hard-invariant failures across the 15 validation cases and real-work samples.
- No regression in output-mode compliance.
- No regression in protected literals, facts, scope, certainty, commitments, or citations.
- Detector and authorship requests remain handled without guarantees or unsupported inference.
- Default personal voice and Indian English behavior remain acceptable.
- Mean blind-review quality is no worse than baseline by more than 0.25 on a 5-point scale.
- No individual high-risk case drops by more than 1 point.
- The measured common-path reduction is at least 25%, unless a smaller reduction removes a clear routing inefficiency with no quality loss.
- The candidate does not compensate for shorter instructions by loading more optional references in routine cases.

### Reject or restore a rule when any condition occurs

- A protected detail changes or disappears.
- The candidate invents content, changes certainty, or weakens/strengthens a claim.
- A prohibited detector guarantee or authorship inference appears.
- A required mode contract is violated.
- Personal voice becomes generic, stereotyped, or less accurate.
- The agent repeatedly loads optional references unnecessarily.
- Token reduction comes mainly from shifting text to a reference that is then loaded on every task.

When a regression occurs, restore the smallest rule that addresses the failure, place it at the earliest relevant decision point, and rerun the failed case plus its nearest neighboring cases before rerunning the full suite.

## 9. Results record template

Create one row per run:

| Field | Value |
|---|---|
| Case/sample ID | |
| Baseline or candidate | |
| Model/version | |
| Skill commit/version | |
| Date | |
| References loaded | |
| Input tokens | |
| Output tokens | |
| Total tokens | |
| Hard invariants | Pass/Fail |
| Correctness | Pass/Fail |
| Completeness | Pass/Fail |
| Instruction compliance | Pass/Fail |
| Naturalness/voice | 1-5 |
| Reviewer notes | |

Summarize results with median token usage, worst-case token usage, pass rate, quality score, and reference-loading frequency.

## 10. Recommended implementation order

1. Approve this plan and freeze the baseline.
2. Create a separate candidate copy; do not overwrite the baseline.
3. Consolidate `SKILL.md` only.
4. Measure tokens and run the four-case smoke test.
5. Run all 15 validation cases.
6. Tighten the personal profile and repeat measurements and tests.
7. Tighten the LinkedIn profile and repeat measurements and tests.
8. Run routing tests and real-work samples.
9. Accept changes individually; restore rules responsible for regressions.
10. Promote the candidate only after all quality gates pass.
11. Record final counts, observed runtime savings, accepted changes, rejected changes, and remaining risks in this document or a linked results report.

## 11. External guidance used

The plan applies these shared recommendations from the supplied sources:

- Metadata is the always-loaded discovery surface; complete instructions load after activation.
- References and resources should load only when needed through progressive disclosure.
- Keep `SKILL.md` concise and assume the model already understands generic concepts.
- Keep references one level from `SKILL.md` and use explicit load conditions.
- Test with representative tasks, identical controls, and feedback loops.
- Prefer observed file-access behavior and real usage over bundle size alone.

Sources reviewed:

- [OpenAI: Skills tool guide](https://developers.openai.com/api/docs/guides/tools-skills?utm_source=chatgpt.com) - unavailable from the audit environment on 2026-10-28; retain for implementation review.
- [OpenAI Cookbook: Skills in the API](https://developers.openai.com/cookbook/examples/skills_in_api?utm_source=chatgpt.com) - unavailable from the audit environment on 2026-10-28; retain for implementation review.
- [Anthropic: Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices?utm_source=chatgpt.com)
- [Anthropic: Agent Skills overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview?utm_source=chatgpt.com)
- [Agent Skills open specification repository](https://github.com/agentskills/agentskills?utm_source=chatgpt.com)

The Anthropic token figures are architecture examples for Anthropic runtimes, not measurements of this VS Code skill. This plan uses locally measured `tiktoken` values for consistent baseline/candidate comparison and requires runtime-reported usage where available.