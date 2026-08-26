---
name: dnd-wiki-obsidian
description: Create and edit valid DnD Wiki Obsidian plugin blocks, content types, parameters, and source-version syntax.
---

# DnD Wiki Obsidian Plugin

Use this skill only for the DnD Wiki Obsidian plugin's syntax and content blocks. General Obsidian note editing belongs to the separate Obsidian note-taking skill.

## Source Versions

The standard source keys are:

- `5e`
- `2024`

Use the source version that matches the requested rules content. The block types and parameter rules are the same for both sources.

````markdown
```dnd2024-spell
Fireball
```

```dnd5e-spell
Fireball
```
````

## Individual Content Types

These content types accept no parameters:

- `spell`
- `feat`
- `magicitem`
- `background`
- `lineage`
- `class`

They contain one name or identifier per line.

````markdown
```dnd2024-spell
Fireball
Mage Hand
```

```dnd2024-feat
Alert
Lucky
```
````

Do not add parameters to individual content blocks. Use the corresponding list block when filtering is required.

## Spell Lists

Block type:

```text
dnd<VERSION>-spelllist
```

Supported parameters:

- `level:`
- `class:`
- `school:`
- `addspells:`
- `removespells:`
- `search:`
- `searchMode:`

### `level:`

Legal values:

- `all`
- `0`
- `1` through `9`

Ranges and comma-separated values are supported.

````markdown
```dnd2024-spelllist
level: all
```

```dnd2024-spelllist
level: 1, 2, 3
```

```dnd2024-spelllist
level: 2-5
```
````

### `class:`

Legal values:

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

Multiple classes act as alternatives.

````markdown
```dnd2024-spelllist
class: Wizard, Sorcerer
```
````

### `school:`

Legal values:

- `Abjuration`
- `Conjuration`
- `Divination`
- `Enchantment`
- `Evocation`
- `Illusion`
- `Necromancy`
- `Transmutation`

Multiple schools act as alternatives.

````markdown
```dnd2024-spelllist
school: Evocation, Abjuration
```
````

### `addspells:` and `removespells:`

Both accept free-text spell names.

````markdown
```dnd2024-spelllist
level: 1-3
class: Wizard
addspells: Healing Word
removespells: Fireball
```
````

### `search:`

Accepts free-text search queries. Spaces inside one `search:` value stay together as part of that single query.

For example, to search for fire damage, use one query:

````markdown
```dnd2024-spelllist
search: fire damage
```
````

Do not split that into `search: fire` and `search: damage` unless you specifically want two separate search clauses.

Multiple `search:` parameters are allowed. Each parameter creates a separate search clause that is combined using `searchMode:`.

### `searchMode:`

Legal values:

- `Or` — match any separate search clause
- `And` — require every separate search clause

````markdown
```dnd2024-featlist
search: strength
search: dexterity
searchMode: Or
```

```dnd2024-spelllist
search: range self
search: heals
searchMode: And
```
````

Use `Or` when you want alternatives, such as feats that mention Strength **or** Dexterity. Use `And` when you want one result to satisfy multiple separate queries, such as a spell whose text includes both a self range and healing.

## Other List Types

The following list types support only `search:` and `searchMode:`:

- `dnd<VERSION>-featlist`
- `dnd<VERSION>-backgroundlist`
- `dnd<VERSION>-lineagelist`

````markdown
```dnd2024-featlist
search: constitution
search: strength
searchMode: Or
```

```dnd2024-backgroundlist
search: criminal
searchMode: Or
```

```dnd2024-lineagelist
search: elf
searchMode: Or
```
````

Do not use parameters such as `class:` with these list types.

## Magic Item Lists

Block type:

```text
dnd<VERSION>-magicitemlist
```

Supported parameters:

- `level:`
- `type:`
- `search:`
- `attuned:`
- `searchMode:`

### `level:`

Legal values:

- `Common`
- `Uncommon`
- `Rare`
- `Very-Rare`
- `Legendary`
- `Artifact`
- `Unique`
- `Other`

Multiple values act as alternatives.

### `type:`

Legal values:

- `Armor`
- `Potion`
- `Ring`
- `Rod`
- `Scroll`
- `Staff`
- `Wand`
- `Weapon`
- `Wondrous Item`

Multiple values act as alternatives.

### `attuned:`

Legal values:

- `Required`
- `Not-Required`

````markdown
```dnd2024-magicitemlist
level: Uncommon, Rare
type: Ring, Wondrous Item
attuned: Required
search: teleport
searchMode: And
```
````

## Class Information

Block type:

```text
dnd<VERSION>-classinfo
```

Supported parameters:

- `class:`
- `subinfo:`
- `section:`
- `sectionFrom:`

There is no `search:` parameter for `classinfo`.

### `class:`

Use one of the standard class values:

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

### `subinfo:`

Free text. Multiple `subinfo:` lines can construct a page path.

````markdown
```dnd2024-classinfo
class: Blood Hunter
subinfo: Mutant
subinfo: Mutagens
```
````

### `section:`

Free text selecting a matching section.

````markdown
```dnd2024-classinfo
class: Fighter
subinfo: Battle Master
section: Maneuvers
```
````

### `sectionFrom:`

Free text selecting a heading and following headings at the same level according to the plugin's section behavior.

````markdown
```dnd2024-classinfo
class: Warlock
subinfo: Eldritch Invocation
sectionFrom: Agonizing Blast
```
````

`section:` and `sectionFrom:` can be combined and repeated.

## Custom Pages

Custom pages use:

```text
dnd<VERSION>-custom
```

Supported parameters:

- `source:`
- `section:`
- `sectionFrom:`

All three parameters accept free text.

### `source:`

Specifies the wiki page or path. The value is appended directly to the configured base URL. Do not modify or reinterpret the path.

````markdown
```dnd2024-custom
source: equipment:weapon
```
````

### `section:` and `sectionFrom:`

````markdown
```dnd2024-custom
source: equipment:weapon
section: Mastery Properties
```

```dnd2024-custom
source: equipment:weapon
sectionFrom: Mastery Properties
```
````

If neither parameter is supplied, the complete custom page is displayed.

Do not invent custom source paths.

## Parameter Rules

Always distinguish between enumerated and free-text parameters.

### Enumerated parameters

- `spelllist.level`
- `spelllist.class`
- `spelllist.school`
- `spelllist.searchMode`
- `magicitemlist.level`
- `magicitemlist.type`
- `magicitemlist.attuned`
- `magicitemlist.searchMode`
- `classinfo.class`

### Free-text parameters

- `addspells:`
- `removespells:`
- `search:`
- `subinfo:`
- `section:`
- `sectionFrom:`
- `custom.source:`

Never invent additional parameters.

````markdown
```dnd2024-featlist
class: Fighter
```
````

The example above is invalid because `featlist` supports only `search:` and `searchMode:`.

````markdown
```dnd2024-spell
class: Wizard
```
````

The example above is invalid because individual `spell` blocks accept no parameters.

## Block Selection

Use the most specific available block:

- Specific entries: `spell`, `feat`, `magicitem`, `background`, `lineage`, `class`
- Filtered collections: `spelllist`, `featlist`, `backgroundlist`, `lineagelist`, `magicitemlist`
- Class or subclass information: `classinfo`
- Wiki pages without a dedicated content type: `custom`

Apply the same syntax to `5e` and `2024` by replacing the source key:

````markdown
```dnd5e-spelllist
level: 1-3
class: Wizard
```
````
