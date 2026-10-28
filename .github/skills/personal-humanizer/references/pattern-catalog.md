# Pattern catalog

Use this catalog as judgment guidance, not as a forbidden-word list. Edit a pattern only when it creates a concrete problem with accuracy, clarity, audience fit, voice or required format. Association with AI-generated text is not sufficient.

## Development sources

This catalog was developed with reference to the following field guides (accessed 2026-10-28):

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), a descriptive and evolving Wikipedia-specific advice page rather than a policy or general-purpose style guide.
- [Signs of AI Writing](https://github.com/softaworks/agent-toolkit/blob/main/skills/writing-clearly-and-concisely/signs-of-ai-writing.md) from `softaworks/agent-toolkit`, which adapts and organizes many of the same observations for an agent-writing context.

These sources informed the pattern taxonomy and examples; they are not runtime authorities. Their observations may be context-specific, may change over time and must not be converted into bans, detector claims or evidence of authorship. The rules below control how the skill applies them.

Each entry identifies its primary purpose:

- **Accuracy risk:** May add unsupported content or alter what the source means.
- **Clarity problem:** May obscure, inflate or repeat the source's point.
- **Contextual style tendency:** May sound mechanical in context but can be intentional and effective.
- **Artifact:** Material from a chat or drafting process that does not belong in the finished text.
- **Detection clue only:** A correlation with some AI-generated text that is not, by itself, a writing defect.

**Actionability** states whether the pattern can justify an edit on its own. A detection clue alone is never independently actionable. Preserve any pattern that serves the meaning, audience, voice or required style.

## Always fix

### Chatbot residue

**Purpose:** Artifact  
**Actionability:** Independently actionable when the wording addresses the chatbot user rather than the intended reader.

Remove greetings, praise, offers to continue and closers that belong to the chat rather than the finished text. Examples include "Great question," "I hope this helps" and "Let me know if you want more."

Keep genuine greetings, thanks and signoffs addressed to the intended recipient.

### Unsupported additions

**Purpose:** Accuracy risk  
**Actionability:** Independently actionable when the rewrite invents content or exceeds the source.

Remove facts, citations, experiences, emotions, statistics and opinions added by the rewrite without support from the source or user. Do not convert uncertainty into certainty or infer a missing actor, relationship or motive.

Do not assume an existing source claim is false or unsupported merely because it lacks a citation or resembles a known pattern. Preserve it, ask for evidence when necessary, or flag it in review-only mode. State that the source lacks a fact only when the supplied material establishes that omission and it matters to the reader.

### Borrowed authority

**Purpose:** Accuracy risk and clarity problem  
**Actionability:** Independently actionable when the authority or attributed view is unsupported.

Revise phrases such as "experts argue," "industry reports" or lists of prestigious publications when they do not identify what a relevant source actually said. Keep named evidence and its supported claim.

Never convert an attributed claim into an unattributed fact. If support cannot be assessed from the supplied material, preserve the attribution or flag it rather than silently deleting it.

## Usually fix

### Staging instead of stating

**Purpose:** Clarity problem  
**Actionability:** Edit when the staging delays the point or adds emphasis without meaning.

Remove run-ups such as "Let's dive in," "Here's the thing" and "What really matters is" when the sentence can state the point directly.

Revise hidden-truth formulas such as "at its core," "the heart of the matter" and "X is the language of Y" when they dress up an ordinary claim without adding detail.

### Empty contrasts and objections

**Purpose:** Clarity problem  
**Actionability:** Edit when the rejected position is not relevant to the audience or argument.

Revise "not only X but Y," "I'm not saying" and "you might think" when the negative half answers no real belief or adds no useful correction. Keep a contrast or objection when both sides carry information or the audience is likely to weigh it.

### Repetitive closers

**Purpose:** Clarity problem  
**Actionability:** Edit when the closer adds no fact, consequence or intentional emphasis.

Remove a short final sentence that only repeats or announces the importance of the preceding point. Keep a short sentence when it adds a consequence, fact or deliberate emphasis appropriate to the voice.

### Inflation and sales language

**Purpose:** Clarity problem; accuracy risk when significance is unsupported  
**Actionability:** Edit when promotional framing exaggerates or obscures the specific fact.

When the user asks to neutralize promotional copy, replace authorized promotional framing with the specific fact. Otherwise preserve explicit source claims, including superlatives, rankings and statements of commitment, unless they can be rephrased without changing meaning. Review words such as "pivotal," "robust," "vibrant," "showcase" and "evolving landscape" in context rather than deleting them mechanically.

Use simple verbs when phrases such as "serves as," "stands as," "functions as" or "boasts" add no precision.

### Vague relationships

**Purpose:** Clarity problem; accuracy risk if the rewrite infers a more specific relationship  
**Actionability:** Edit only when the source supports clearer wording.

Replace "associated with," "linked to" or "connected with" when the source gives the actual relationship. Keep general wording when the source does not support anything more specific.

### Decorative formatting

**Purpose:** Clarity problem and contextual style tendency  
**Actionability:** Edit when decoration obscures hierarchy or conflicts with the target format.

Remove bold labels, title case headings, decorative emoji, repeated horizontal rules and headings that are immediately restated. Keep formatting that expresses real hierarchy or is required by the target format.

## Context dependent

### Repetition and parallel structure

**Purpose:** Contextual style tendency  
**Actionability:** Not independently actionable; require nearby evidence that the repetition is mechanical or redundant.

Repeated openings, fragments and groups of three can sound formulaic, but they can also create rhythm or emphasis. Edit them only when several nearby instances feel mechanical or items add no distinct information.

### Passive voice

**Purpose:** Contextual style tendency  
**Actionability:** Not independently actionable; edit only when naming the actor improves clarity and the source identifies that actor.

Use active voice when naming the actor makes the sentence clearer. Keep passive voice when the actor is unknown, irrelevant or intentionally de-emphasized. Never invent an actor.

### Hedges and qualifications

**Purpose:** Accuracy risk and contextual style tendency  
**Actionability:** Stacked filler may be edited, but supported uncertainty must be preserved.

Reduce stacked hedges such as "could potentially possibly" while preserving uncertainty supported by the source. Keep legal, medical, scientific and safety qualifications.

### Dashes and hyphens

**Purpose:** Contextual style tendency  
**Actionability:** Not independently actionable; edit only when another construction is clearer or required by house style.

Frequent sentence dashes can hide the relationship between clauses. Replace them when a period, comma, colon or parentheses is clearer. Preserve proper names, technical compounds, commands, paths, codes, dates and unambiguous compound modifiers.

### Background and document narration

**Purpose:** Clarity problem and contextual style tendency  
**Actionability:** Edit when the intended reader already has the context or the narration does not affect interpretation.

In replies, remove background the recipient already knows and lead with the answer. Keep methodology, sourcing notes or document conventions when they change how the reader should interpret or use the material.

## Detection clues only

Word choice, punctuation, sentence length and formatting may correlate with output from particular models or periods. Treat these observations only as prompts to inspect the passage. They do not justify edits unless the wording also creates an accuracy, clarity, audience, voice or format problem.

Do not replace one suspected model pattern with another, and do not lower writing quality merely to make authorship harder to classify.
Do not infer or claim authorship from these patterns. This catalog is primarily based on English-language observations and must not be transferred mechanically to other languages or regional varieties.

## Do not edit a watched pattern when it is

- Inside a quotation, title, proper name or established technical term
- Being discussed rather than used
- Deliberate repetition for rhythm, persuasion or emphasis
- Required for precision, qualification or a target style guide
- Consistent with a representative writing sample
- A genuine greeting, thanks or signoff for the intended recipient

Preserve specific details, mixed feelings, uncertainty, humor, asides and stylistic quirks that carry the writer's voice.