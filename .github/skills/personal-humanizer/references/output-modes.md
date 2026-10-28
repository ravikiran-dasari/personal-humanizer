# Output modes

Choose the mode before editing because it controls both the work and the response format.

## Pasted text

Use when the user supplies prose directly and asks for a rewrite.

Return the revised text first without a preamble. Add a short "Main edits" list only when substantial structural or tonal changes would benefit from explanation. Add a brief "Flags" note only when the user must resolve an ambiguity or missing fact.

If the text already sounds natural, keep it nearly unchanged and say so after the revised text.

Use this shape:

```text
[Revised text]

Main edits:                 # Optional; omit for light edits
- [Substantial change and why it helped]

Flags:                      # Optional; include only when user action is needed
- [Ambiguity or missing fact]
```

## File

Use when the user asks to edit a named file.

Run the complete workflow, write only the finished prose to the file and summarize the changes in chat. Preserve frontmatter, code, commands, paths, URLs, data, link targets and other nonprose content unless the user explicitly asks to edit them.

The file must contain only the revised artifact. Use this shape in chat after the edit:

```text
Updated [file]. [Brief summary of the material changes.]
```

## Embedded

Use for text that another tool or workflow will insert into a commit, pull request, caption, message or document.

Return only the finished text. Do not add a preamble, edit notes, headings or offers to continue unless they are part of the requested artifact.

Use this shape, with no surrounding commentary:

```text
[Finished text]
```

## Review only

Use only when the user asks for critique, diagnosis or suggested edits without requesting a rewrite.

List the most consequential issues first. Ground each issue in a specific phrase or structure and explain its effect briefly. Do not rewrite the full text unless requested.

Use this shape:

```text
- "[Specific phrase or structure]": [Concrete problem and its effect]
- "[Specific phrase or structure]": [Concrete problem and its effect]
```

## Ambiguity

Ask a question only when different answers would materially change meaning, audience, commitments or required formality. Otherwise make the smallest reasonable assumption and preserve the source.

A blocking ambiguity overrides the normal output contract. Ask the necessary question before returning embedded or file content.