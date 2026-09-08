---
name: obsidian-note-taking
description: Create, reorganize, and edit notes in Obsidian vaults while preserving properties, wikilinks, embeds, callouts, and plugin-specific Markdown. Use for note-writing tasks inside an Obsidian vault; do not use for generic Markdown outside a vault.
---

# Obsidian Note Taking

Create clear, readable Obsidian notes using standard Markdown and Obsidian-specific syntax.

## Editing and authorization

- Edit a vault file only when the user explicitly asks to write, record, add, reorganize, or otherwise change content.
- Do not interpret a factual statement or conceptual question as permission to edit a file.
- If writing intent is unclear, ask whether the user wants the information recorded and suggest the relevant note.
- Read the target note and enough nearby context to understand its structure before editing.
- Prefer small, targeted changes over broad rewrites.
- Do not rename or delete notes without explicit instruction.
- Respect workspace-specific instructions in addition to this skill.

## File operations

- Use `apply_patch` for every addition or modification to Markdown and other text files in the vault.
- Create new text files with `apply_patch` and `*** Add File`.
- Treat vault text files as UTF-8. Preserve Unicode characters and existing encoding.
- Never rely on shell-default encoding when writing vault text.
- If `apply_patch` is technically unsuitable, use an explicitly UTF-8-safe method and verify the resulting file before responding.
- Preserve unrelated content and formatting.

## Reporting changes

At the end of every response that changes vault files, report the affected files under these labels:

- **Added**
- **Changed**
- **Deleted**

List each file as an Obsidian wikilink. Write `None` for an empty category.

## Note structure

- Treat the file name as the note title.
- Do not repeat the file name as a top-level heading unless a visible in-note title is specifically useful.
- Use headings to organize the note’s actual content.
- Prefer short paragraphs and focused lists.
- Keep one main concept per note when practical.
- Preserve the author’s terminology unless correction or rewriting was requested.
- Do not invent facts. Clearly label uncertainty, assumptions, and proposals.

## Links

Use wikilinks for content inside the vault:

- `[[Note Name]]`
- `[[Note Name|Display Text]]`
- `[[Note Name#Heading]]`
- `[[Note Name#^block-id]]`
- `[[#Heading in the same note]]`

Use standard Markdown links for external resources:

- `[Link text](https://example.com)`

Add internal links only when the relationship is meaningful. Before adding one, verify that its target already exists or is intentionally planned.

## Obsidian syntax

- Use callouts when they materially improve scanning or distinguish important content:

  `> [!note]`

- Use `==highlighted text==` sparingly for meaningful emphasis.
- Preserve valid embeds, block IDs, block references, comments, tags, and other Obsidian syntax.
- Preserve YAML frontmatter and Obsidian properties unless the requested change requires modifying them.
- Preserve property names, value types, and existing conventions.

## Structured and plugin-specific content

Preserve specialized content such as:

- Dataview and DataviewJS blocks
- Excalidraw data
- fenced-blocks (```)
- Mermaid diagrams
- Tasks syntax
- Templater expressions
- Other plugin-specific fenced blocks or directives

Do not replace structured, executable, or visual data with ordinary prose unless the user explicitly requests that conversion.

## Boundary whitespace

A Markdown file must not begin or end directly with a fenced code block or callout.

- Leave at least one blank line before an opening fence or callout at the start of a file.
- Leave at least one blank line after a closing fence or callout at the end of a file.
- When creating an otherwise empty file containing only a fenced block or callout, include both the leading and trailing blank lines.