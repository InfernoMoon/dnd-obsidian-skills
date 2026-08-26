---
name: obsidian-note-taking
description: Create and edit readable Obsidian notes using standard Markdown and Obsidian-specific links, callouts, embeds, and formatting.
---
# Obsidian Note Taking

Use this skill when creating, reorganizing, or editing notes in an Obsidian vault.

## Mandatory File-Editing and Reporting Rules

- For every Markdown or other text-file addition or modification in the vault, **always use `apply_patch`** so the user can inspect the diff.
- Use `apply_patch` with `*** Add File` when creating a new text file.
- Treat vault text files as UTF-8. Preserve Unicode characters and existing encoding; never use shell-default encoding for vault text files.
- If `apply_patch` is technically unsuitable, use an explicit UTF-8-safe method and verify the result before responding.
- Do not edit files merely because the user states a fact or asks a conceptual question. Edit only when the user explicitly asks to write, add, record, update, or otherwise change a file, or when that intent is heavily implied. If the intent is unclear, ask whether the user wants it written down and propose which file or files should be changed.
- At the end of every response that changes files, list the files that were **Added**, **Changed**, and **Deleted**, using Obsidian wikilinks.

## Markdown and Links

- Write content using standard Markdown for structure, including headings, paragraphs, lists, tables, blockquotes, and code blocks.
- Link related notes with wikilinks such as `[[Note Name]]` for internal vault connections.
- Use standard Markdown links such as `[text](https://example.com)` for external URLs.
- When choosing between link formats, use wikilinks for notes within the vault and Markdown links for external URLs.

### Internal Links

- `[[Note Name]]` — link to a note
- `[[Note Name|Display Text]]` — link to a note with custom display text
- `[[Note Name#Heading]]` — link to a heading
- `[[Note Name#^block-id]]` — link to a block
- `[[#Heading in same note]]` — link to a heading in the current note

## Note Structure

- When the Obsidian interface already displays the file name as the note title, do not repeat it as a redundant top-level heading unless a visible title inside the note is specifically useful.
- Use headings to organize the note's actual content.
- Keep one main concept per note when practical.

## Obsidian-Specific Formatting

- Add callouts for highlighted information using `> [!type]` syntax.
- Use callouts when they improve scanning or distinguish important information from ordinary prose.
- `==Highlighted text==` — highlight text.
- Preserve valid Obsidian embeds, block references, and other Obsidian syntax when editing.
- Treat the file name as the note title; do not add a redundant top-level heading just to repeat it, since Obsidian already displays the file name as the title.
- Preserve Dataview, ccard, statblock, Excalidraw and similar code blocks.
- Do not replace Excalidraw data with ordinary Markdown.

## Note Quality and Safety

- Prefer clear headings, short paragraphs, and focused lists.
- Link related notes when the relationship is meaningful; do not add links merely for decoration.
- Preserve the author's terminology and content unless correction or rewriting is requested.
- Do not invent facts when editing knowledge notes; mark uncertainty or proposals clearly.
- Preserve existing Dataview, ccard, statblock, Excalidraw, and other specialized blocks.
- Do not replace structured or visual data with ordinary Markdown.

## Editing Workflow

- Read the relevant note and nearby context before editing.
- Prefer small, targeted changes over broad rewrites.
- Do not rename or delete notes without explicit instruction.
- Verify new internal links point to existing or intentionally planned notes.
- Use UTF-8-safe file handling when reading and writing notes; preserve existing Unicode characters and avoid shell-default encodings that can create mojibake.
- Respect any workspace-specific instructions separately from this reusable skill.
