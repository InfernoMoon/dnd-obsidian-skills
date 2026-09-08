---
name: fantasy-statblocks
description: Create, edit, recall, and troubleshoot Fantasy Statblocks creatures in Obsidian using either inline YAML or reusable JSON storage. Use for Basic 5e statblocks, variants, overrides, and saved custom creatures; ask which storage method the user prefers before creating a new creature.
---

# Fantasy Statblocks

Create and maintain Fantasy Statblocks creatures using the Basic 5e Layout.

Use the general Obsidian note-taking skill for vault discovery, UTF-8 handling, `apply_patch`, surrounding Markdown, and change reporting.

## Choose the storage method

Before creating a new creature, ask:

> Should the creature be defined inline in this note, or saved in the plugin’s JSON so it can be reused from other notes?

Do not ask when:

- The user already chose a method.
- The user is editing an existing creature; preserve its current method unless conversion was requested.
- The request is read-only troubleshooting or explanation.

| Method | Advantages | Drawbacks |
| --- | --- | --- |
| Inline YAML | Easy for the user to find and edit; self-contained in the note; no plugin-data editing or vault reload | Not reusable elsewhere through a `monster:` reference unless separately saved |
| Plugin JSON | Reusable from multiple notes; compact `monster:` references; one centralized creature definition | Harder to edit manually; modifying plugin data requires extra validation and usually a vault reload |

The choice changes where data is stored, so do not silently select one when the user has not expressed a preference.

## Inline statblocks

Define an inline creature directly inside a Markdown note:

````markdown
```statblock
layout: Basic 5e Layout
name: HB Example Creature
size: Medium
type: Humanoid
alignment: Neutral
ac: 15
hp: 45
hit_dice: 6d8 + 18
speed: 30 ft.
stats: [16, 14, 16, 10, 12, 8]
saves:
  - str: 5
skillsaves:
  - Athletics: 5
damage_vulnerabilities:
damage_resistances:
damage_immunities:
condition_immunities:
senses: passive Perception 11
languages: Common
cr: "2"
traits:
  - name: Example Trait
    desc: The creature has an example trait.
actions:
  - name: Example Attack
    desc: "Melee Weapon Attack: +5 to hit, reach 5 ft., one target. Hit: 8 (1d10 + 3) slashing damage."
    attack_bonus: 5
    damage_dice: 1d10
    damage_bonus: 3
bonus_actions: []
reactions: []
legendary_actions: []
spells: []
```
````

All fields are optional. Include only fields that apply to the creature; remove unused fields instead of filling them with meaningless placeholders.

### Inline field types

- `layout`: Use `Basic 5e Layout` unless another layout was explicitly requested.
- `image`: Use an Obsidian image wikilink when provided.
- `ac` and `hp`: Numbers.
- `stats`: Six numbers in STR, DEX, CON, INT, WIS, CHA order.
- `fage_stats`: Nine Fantasy AGE values. Omit this field for an ordinary 5e creature.
- `cr`: Quote fractional values such as `"1/2"`.
- `saves`: List of ability-to-modifier mappings.
- `skillsaves`: List of skill-to-modifier mappings.
- `spells`: List of spellcasting information supported by the plugin.
- `traits`, `actions`, `bonus_actions`, `reactions`, and `legendary_actions`: Lists of named entries with descriptions.

Trait and action entries use:

```yaml
- name: Entry Name
  desc: Entry description.
```

For attacks, optional structured fields include:

```yaml
attack_bonus: 5
damage_dice: 1d10
damage_bonus: 3
```

Keep the complete playable attack text in `desc`. Quote YAML values containing syntax-sensitive characters such as `:` or `*`.

Inline statblocks do not require a JSON edit or vault reload.

## Reusable JSON creatures

Reusable custom creatures are stored in:

```text
.obsidian/plugins/obsidian-5e-statblocks/data.json
```

Read the complete existing file before editing it. Plugin versions and local conventions may differ.

Add or update only the intended entry in the top-level `monsters` array. Each custom entry is a two-item array:

```json
[
  "HB Creature Name",
  {
    "name": "HB Creature Name",
    "bestiary": false
  }
]
```

- The first item is the exact lookup name.
- The second item is the creature object.
- Update a matching entry instead of creating a duplicate.
- Preserve all unrelated monsters and top-level data.
- Do not modify layouts, defaults, plugin settings, version information, paths, or other top-level properties.
- Follow the types and field conventions already used by nearby custom monsters.
- Use `stats` as six numbers in standard ability-score order.
- Preserve the local JSON representation of `cr`; custom data commonly stores it as a string.
- Use numeric types for structured attack fields.
- Use `bestiary: false` for campaign-created creatures unless the existing vault uses another convention.

Reference a saved creature from Markdown with:

````markdown
```statblock
monster: "HB Creature Name"
```
````

The JSON entry key, object `name`, and Markdown `monster:` value must match exactly.

## Existing creatures and variants

Recall an existing creature with:

````markdown
```statblock
monster: "Creature Name"
```
````

A `monster:` reference may be combined with inline fields to override selected values:

````markdown
```statblock
monster: "Ancient Black Dragon"
name: Paarthurnax
hp: 420
```
````

Use `extends` when the creature should retain a live relationship to a base creature.

Use list operators such as `traits+`, `actions+`, `traits-`, or `actions-` only when deliberately adding to or removing from an inherited list.

Do not replace a reusable JSON creature with duplicated inline definitions unless the user requests conversion.

## Creature-writing conventions

- Prefix newly designed campaign creatures with `HB`, unless the user specifies another name.
- Keep the JSON key, object `name`, and Markdown reference consistent.
- Write compact, playable statblocks.
- Include mechanics needed to run the creature, but omit redundant rules text.
- Do not reproduce full spell descriptions inside the statblock.
- When requested and the `dnd-wiki-obsidian` skill is available, add separate DnD Wiki spell references after the statblock.
- Avoid resistance to bludgeoning, piercing, and slashing simultaneously unless the user explicitly wants it or the creature’s design strongly requires it.
- Preserve meaningful player counterplay.
- When designing a creature, infer reasonable statistics from the requested concept and briefly disclose important assumptions outside the block.
- When editing an existing creature, do not invent unrelated mechanics.

## Validation

For both storage methods:

1. Confirm the requested storage method.
2. Confirm that the statblock uses supported Basic 5e fields.
3. Confirm that `stats` contains six numbers in the correct order.
4. Confirm YAML indentation and quote syntax-sensitive values.
5. Confirm every trait and action has a `name` and `desc`.
6. Confirm structured attack bonuses and damage bonuses are numeric.
7. Preserve unrelated note content and existing statblocks.

For JSON storage additionally:

1. Parse the completed file as JSON.
2. Confirm that only the intended `monsters` entry changed.
3. Confirm that no duplicate creature key was introduced.
4. Confirm that the JSON key, object `name`, and Markdown reference match.
5. Confirm that unrelated top-level settings remain unchanged.

## Reload after JSON changes

A vault reload is needed only after manually changing the plugin JSON.

After all JSON and Markdown edits are complete and verified, run:

```text
obsidian vault="Vault Name" reload
```

Replace `Vault Name` with the actual vault name.

Do not reload after an inline-only edit. If the command-line interface is unavailable, tell the user to enable **Settings → General → Command line interface** or reload the vault manually.