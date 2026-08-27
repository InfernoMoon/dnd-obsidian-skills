---
name: callout-tracking
description: Create, edit, and maintain Obsidian callouts and Callout Tracker overview blocks for organizing campaign ideas, notes, todos, hooks, rules, and clues without relying on tags or properties.
---

# Callout Tracking

Use this skill when creating, reviewing, organizing, or cleaning up tracked callouts in the campaign vault.

## Use Callout Tracker

To create a dedicated overview note, such as `Callout Tracker.md`, use:

```callout-tracker
callouts: callountname, anothercallountname
rootfolder: Myroot
```

The plugin scans the selected folder and displays matching callouts grouped by type. Each result is clickable and opens the source note at the callout’s line.

`rootfolder:` is optional. If omitted, the plugin uses its configured default root folder. An empty default root folder searches the entire vault.

`callouts:` Enter one or more callout names here, separated by commas. The order determines how the results are grouped: callouts of the first type appear first, followed by the next types.

## Add a search section

Add a `search:` line to a `callout-tracker` block:

```callout-tracker
callouts: todo, idea
rootfolder: Campaign
search: tavern
```

Only callouts containing `tavern` in their header or body are displayed. Searches are case-insensitive.

Remove the `search:` line or leave it empty to show all selected callouts.

Multiple overview blocks can be used for different purposes:

```callout-tracker
callouts: todo
search: unresolved
```

```callout-tracker
callouts: idea, hook
search: village
```

While editing a block, the plugin suggests `callouts:`, `rootfolder:`, and `search:`. After `callouts:`, it suggests callout names configured in the plugin settings. Suggestions also work after commas.

Only use search and rootfolder when it makes sense. If they are not needed no not add them.

## Callout meanings

- `[!idea]` — proposed or speculative content.
- `[!note]` — important context that should be surfaced, but is not unfinished work.
- `[!todo]` — unfinished preparation, unresolved questions, or a concrete follow-up action.
- `[!hook]` — a possible plot hook, lead, or story opportunity.
- `[!rule]` — a campaign rule, constraint, or agreed decision.
- `[!clue]` — an unresolved clue, discovery, or piece of information to revisit.

Use any custom callout type defined in Callout Tracker settings when it better describes the item.
Additional callout may be mentioned and AGENTS.md

## Rules

- Keep callouts short, specific, and close to the content they describe.
- For `[!idea]`, clearly preserve its proposed status.
- For `[!todo]`, describe the missing decision or action instead of writing a vague reminder.
- For `[!hook]`, record the story opportunity and its relevant context.
- For `[!rule]`, write the rule or decision clearly enough to apply later.
- For `[!clue]`, preserve what is known and identify what remains unresolved.
- Do not use tags or properties for this tracking system.
- Do not duplicate the same tracked item across multiple notes unless the duplication is useful for context.
- When a TODO is completed, remove it or rewrite it to reflect the remaining work.
- Preserve existing links, formatting, and other callouts when editing a note.