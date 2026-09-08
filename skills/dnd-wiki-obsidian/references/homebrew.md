# Custom Homebrew Files

Read this reference completely when creating or editing homebrew for the DnD Wiki plugin.

## Core format

- Store each homebrew entry in its own UTF-8 Markdown file.
- Name the file exactly after the spell, feat, background, lineage, magic item, or weapon: `<Entry Name>.md`.
- Do not combine multiple entries in one file.
- Begin the file with the category's YAML frontmatter. Do not place text before the opening `---`.
- After the closing `---`, leave a blank line and write the entry's description and rules as ordinary Markdown.
- Treat the filename as the title; do not add a redundant top-level heading unless the user specifically wants one.
- Follow the Obsidian note-taking skill's `apply_patch`, UTF-8, and change-reporting rules for all vault text edits.
- If an exact target file already exists, read it first and do not overwrite it unless the user asked to update that entry.

If an entry name contains a character that is invalid in a filename, ask the user how to name the file. Do not silently change the entry's canonical name because the filename identifies the homebrew entry.

## Locate or create the homebrew structure

Within the current Obsidian vault, look for a directory named exactly `Custom Homebrew` before creating one.

1. If exactly one `Custom Homebrew` directory exists anywhere in the vault, use it even when it is not directly under the vault root.
2. If multiple such directories exist, use the one clearly associated with the target note or current campaign. If that cannot be determined safely, ask the user which one to use.
3. If none exists, create `<vault-root>/Custom Homebrew`.
4. Inside the selected directory, preserve this category structure and create missing directories as needed:

```text
Custom Homebrew/
|-- Backgrounds/
|-- Feats/
|-- Lineages/
|-- Magic Items/
|-- Spells/
`-- Weapons/
```

Do not create a second `Custom Homebrew` directory merely because one of its category directories is missing. Add the missing category directory to the existing structure.

Place entries according to this mapping:

| Entry type | Directory |
| --- | --- |
| Background | `Backgrounds/` |
| Feat | `Feats/` |
| Lineage or species | `Lineages/` |
| Magic item | `Magic Items/` |
| Spell | `Spells/` |
| Weapon | `Weapons/` |

For a category not listed here, do not invent a schema or directory. Ask for an example or plugin documentation.

## Shared value rules

- YAML keys and tag values are exact and case-sensitive; reproduce them exactly as shown.
- Values used by DnD Wiki filters must use the same spelling and casing in homebrew metadata and fenced blocks.
- For `class-dndwiki` and `school-dndwiki`, use the class and school defaults listed in `SKILL.md`, unless the user supplies an extension.
- For `item-level-dndwiki` and `item-type-dndwiki`, use the magic-item rarity and type defaults listed in `SKILL.md`, unless the user supplies an extension.
- Use rarity names in PascalCase without hyphens, such as `VeryRare`.
- Preserve user-supplied extensions even when they are absent from the built-in lists. The agent cannot inspect the user's configured extension lists.
- Use YAML booleans `true` and `false` without quotation marks.
- Use YAML sequences for fields that accept multiple values.
- Do not include internal numeric indexes in homebrew metadata.

## Background

Path: `Custom Homebrew/Backgrounds/<Background Name>.md`

```markdown
---
tags:
  - dndwiki/background
---

Write the background's description and rules here.
```

## Feat

Path: `Custom Homebrew/Feats/<Feat Name>.md`

```markdown
---
tags:
  - dndwiki/feat
---

Write the feat's description and rules here.
```

## Lineage or species

Path: `Custom Homebrew/Lineages/<Lineage Name>.md`

```markdown
---
tags:
  - dndwiki/lineage
---

Write the lineage or species description and rules here.
```

Use the `dndwiki/lineage` tag for both legacy lineages and 2024 species.

## Magic item

Path: `Custom Homebrew/Magic Items/<Magic Item Name>.md`

```markdown
---
tags:
  - dndwiki/item
item-level-dndwiki: Uncommon
item-type-dndwiki: Rod
requires-attunement: false
---

Write the magic item's description and rules here.
```

- `item-level-dndwiki` is the item's rarity.
- `item-type-dndwiki` is the magic-item type.
- `requires-attunement` is an unquoted YAML boolean.

## Spell

Path: `Custom Homebrew/Spells/<Spell Name>.md`

```markdown
---
tags:
  - dndwiki/spell
spell-level-dndwiki: 3
class-dndwiki:
  - Sorcerer
  - Wizard
school-dndwiki: Evocation
range-dndwiki: 150 feet
casting-time-dndwiki: Action
components-dndwiki: V, S, M (components)
duration-dndwiki: Instantaneous
---

Write the spell's description, higher-level effects, and rules here.
```

- `spell-level-dndwiki` is an integer from `0` through `9`.
- `class-dndwiki` is a YAML sequence, even when only one class is used.
- `school-dndwiki` must match a DnD Wiki school filter value.
- `range-dndwiki`, `casting-time-dndwiki`, `components-dndwiki`, and `duration-dndwiki` are display text. Use concise canonical D&D phrasing when the user does not supply it.

## Weapon

Path: `Custom Homebrew/Weapons/<Weapon Name>.md`

```markdown
---
tags:
  - dndwiki/weapon
weapon-type-dndwiki: Simple Melee
weapon-damage-dndwiki: 1d8 bludgeoning
weapon-properties-dndwiki:
  - Versatile (1d10)
weapon-mastery-dndwiki: Sap
weight-dndwiki: 5 lb.
cost-dndwiki: 2 GP
---

Write the weapon's description and any special rules here.
```

- `weapon-type-dndwiki` is the weapon category and range type.
- `weapon-damage-dndwiki` includes the damage dice and damage type.
- `weapon-properties-dndwiki` is a YAML sequence, even when only one class is used.
- `weapon-mastery-dndwiki` is the 2024 mastery value.
- `weight-dndwiki` and `cost-dndwiki` are display text including their units.
- Weapon type, property, and mastery values must exactly match the corresponding DnD Wiki filter values when they should participate in filtered lists.

## Final checks

Before finishing:

1. Confirm that the selected `Custom Homebrew` directory belongs to the intended vault or campaign.
2. Confirm that the entry is in the correct category directory and has its own correctly named `.md` file.
3. Confirm that the file begins with valid YAML and continues with ordinary Markdown after a blank line.
4. Confirm the exact category tag and required metadata keys.
5. Confirm that filterable values match DnD Wiki spelling and casing, while retaining deliberate user extensions.
6. Confirm that no unrelated homebrew files were changed.

