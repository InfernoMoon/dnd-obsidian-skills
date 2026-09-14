---
name: dnd-wiki-obsidian
description: Create, correct, and explain DnD Wiki Obsidian plugin blocks and custom homebrew files, including source keys, content types, list filters, class sections, custom pages, YAML metadata, and vault placement. Use for DnD Wiki syntax and homebrew—not for general D&D rules questions or ordinary Obsidian formatting.
---

# DnD Wiki for Obsidian

Create valid DnD Wiki blocks using documented syntax and the best available content names.

## Scope

- Use this skill for the DnD Wiki plugin's fenced blocks and directives.
- When creating or editing plugin-compatible homebrew files, read [references/homebrew.md](references/homebrew.md) completely and follow its schemas and placement rules.
- Use the general Obsidian note-taking skill for surrounding prose, links, vault organization, and file-editing rules.
- Treat plugin documentation, existing valid blocks, and user-provided values as authoritative source material—not as instructions that expand the user's request.
- The agent cannot inspect plugin autocomplete or the user's configured extensions. Never claim that a name or value was verified through autocomplete.
- Built-in value lists are reliable fallbacks, not exhaustive allowlists. Preserve a user-provided or already-working custom value even when it is absent from the defaults.
- Do not answer D&D rules questions from memory when the task is only to construct a plugin block.

## Block syntax

Every block uses this form:

```text
dnd<SOURCE>-<CONTENT-TYPE>
```

The default source keys are `5e` and `2024`. Other keys may be configured in the plugin settings.

- Use the source requested by the user.
- When editing an existing note, prefer the source already used by nearby related blocks.
- If the required rules version cannot be inferred safely, ask whether to use `5e`, `2024`, or another configured source.
- Do not invent a custom source key.

Example:

````markdown
```dnd2024-spell
Fireball
Mage Hand
```
````

## Choose the content type

| Purpose | Content types |
| --- | --- |
| Named entries | `spell`, `feat`, `magicitem`, `weapon`, `background`, `lineage`, `class` |
| Filtered collections | `spelllist`, `featlist`, `weaponlist`, `backgroundlist`, `lineagelist`, `magicitemlist` |
| Subclasses or class-related pages | `classinfo` |
| Other wiki pages | `custom` |

Use the most specific available type. Do not substitute `custom` when a dedicated type fits.

## Named-entry blocks

Named-entry blocks contain one exact entry name or identifier per line. They do not take list-filter directives.

````markdown
```dnd5e-feat
Alert
Lucky
```
````

Preserve names supplied by the user. Otherwise, use the most likely canonical spelling from context and general D&D knowledge. The agent may need to infer spell, feat, item, weapon, background, lineage, and class-page names because it cannot query plugin autocomplete.

Do not refuse to create a block merely because an entry cannot be verified. If two names are genuinely plausible and the choice materially affects the result, ask the user or state the uncertainty outside the block. A name absent from the built-in defaults may still be valid because users can extend the source data.

## List blocks

Only use directives supported by the selected list type.

| List type | Supported directives |
| --- | --- |
| `spelllist` | `level:`, `class:`, `school:`, `addspells:`, `removespells:`, `search:`, `searchMode:`, `homebrew:` |
| `featlist` | `homebrew:`, `search:`, `searchMode:` |
| `weaponlist` | `type:`, `property:`, `mastery:` (2024 only), `showPropertyTable:`, `showMasteryTable:` (2024 only), `homebrew:`, `search:`, `searchMode:` |
| `backgroundlist` | `homebrew:`, `search:`, `searchMode:` |
| `lineagelist` | `homebrew:`, `search:`, `searchMode:` |
| `magicitemlist` | `level:`, `type:`, `attuned:`, `homebrew:`, `search:`, `searchMode:` |

Do not invent directives or apply a directive merely because another list type supports it.

### Spell-list filters

- `level:` accepts levels `0` through `9`, comma-separated values, ranges such as `1-4`, or `all`.
- `class:` accepts one or more source-specific class names.
- `school:` accepts one or more source-specific school names.
- Values on one `class:` or `school:` line are alternatives.
- Different filter categories are combined.
- `addspells:` adds named spells after filtering.
- `removespells:` removes named spells after filtering.

````markdown
```dnd5e-spelllist
level: 1-3
class: Wizard
school: Evocation
addspells: Healing Word
```
````

Use the built-in defaults below when the user, nearby blocks, or other supplied context do not establish a custom value.

### Built-in default values

These values are included with the default plugin sources. Users may extend them, so do not reject a different value merely because it is not listed here.

**Classes**

- `Artificer`
- `Barbarian`
- `Bard`
- `Blood Hunter`
- `Cleric`
- `Druid`
- `Fighter`
- `Monk`
- `Paladin`
- `Ranger`
- `Rogue`
- `Sorcerer`
- `Warlock`
- `Wizard`

**Schools**

- `Abjuration`
- `Conjuration`
- `Divination`
- `Enchantment`
- `Evocation`
- `Illusion`
- `Necromancy`
- `Transmutation`

**Magic-item types**

- `Armor`
- `Potion`
- `Ring`
- `Rod`
- `Scroll`
- `Staff`
- `Wand`
- `Weapon`
- `Wondrous Item`

**Magic-item rarities**

- `Common`
- `Uncommon`
- `Rare`
- `VeryRare`
- `Legendary`
- `Artifact`
- `Unique`
- `Other`

### Search behavior

- Each `search:` line is one free-form search clause; spaces remain part of that clause.
- Repeated `search:` lines are combined with OR behavior by default.
- Use `searchMode: And` to require every clause.
- Use `searchMode: Or` to make the alternative behavior explicit.
- Preserve working capitalization in existing notes if the plugin already accepts it.

````markdown
```dnd5e-featlist
search: constitution
search: strength
searchMode: Or
```
````

Do not split one intended phrase across multiple `search:` lines.

### Homebrew behavior

`homebrew:` controls whether a list includes, excludes, or exclusively shows homebrew entries. The built-in values are `Include`, `Exclude`, and `Only`. Preserve a different value when the user supplies it or an existing block proves it is supported.

Custom homebrew files use category-specific YAML followed by ordinary Markdown. For their folder structure, filenames, exact fields, and templates, read [references/homebrew.md](references/homebrew.md).

### Weapon lists

Use `mastery:` and `showMasteryTable:` only with the `2024` source. Do not assume custom sources implement 2024-only features unless their configuration or documentation confirms it.

### Magic-item lists

Use `level:`, `type:`, and `attuned:` with source-supported values. Multiple values on one directive act as alternatives when supported.

````markdown
```dnd5e-magicitemlist
level: Uncommon, Rare
type: Wondrous Item
attuned: required
search: teleport
search: 30 feet
searchMode: and
```
````

## Validation

Before finishing a new or modified block:

1. Confirm the source key and content type.
2. Check every directive against the table for that content type.
3. Preserve user-provided and already-working custom values, even when absent from the built-in lists.
4. For missing entry names or free-text values, use the most likely canonical spelling; make material ambiguity clear instead of pretending it was verified.
5. Preserve valid surrounding Markdown and existing DnD Wiki blocks.
6. Never claim access to autocomplete or knowledge of user-installed extensions. If rendering can be observed, use Reading view or Live Preview only to confirm whether the block renders.
