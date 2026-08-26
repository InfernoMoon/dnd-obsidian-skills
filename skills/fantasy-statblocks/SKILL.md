---
name: fantasy-statblocks
description: Create, edit, and troubleshoot Obsidian Fantasy Statblocks creatures stored in the vault's custom statblock data and referenced from Markdown.
---
# Fantasy Statblocks — Basic 5e Layout

Use this skill when the user asks for a Fantasy Statblocks creature, variant, recalled monster, or troubleshooting help in Obsidian. Store created or edited custom creatures in `.obsidian/plugins/obsidian-5e-statblocks/data.json`, then place only a normal `statblock` reference in the relevant Markdown note. Do not use other layouts, frontmatter creatures, Dataview, JavaScript, CSS, or unrelated Obsidian formatting unless explicitly requested.

## Storage and Markdown Reference

For a new custom creature, add one entry to the `monsters` array in `.obsidian/plugins/obsidian-5e-statblocks/data.json`. Each entry is a two-item array: the creature's exact name, followed by its creature object. Use the existing JSON structure and preserve all unrelated monsters and top-level settings.

Only edit creature entries inside `monsters`. Do not modify `defaultLayouts`, `layouts`, `default`, plugin settings, version data, paths, or any other top-level property. When editing an existing creature, update the matching entry rather than creating a duplicate.

Use JSON types appropriate to the plugin data file: `stats` is an array of six numbers, `cr` is a string, numeric attack fields are numbers, and empty optional fields are empty strings when the surrounding file uses that convention. Use `bestiary: false` for campaign-created custom creatures unless an existing local convention requires otherwise.

After adding or editing the JSON creature, add or update this reference in the relevant Markdown note:

````markdown
```statblock
monster: "Creature Name"
```
````

The `monster` value must exactly match the creature name/key in `data.json`. Do not duplicate the full creature YAML inline in the note.

## Custom Creature JSON Structure

Use only fields supported by the Basic 5e Layout and the existing custom data format. Omit unused optional fields when the file's existing convention permits it.

- Identity: `image`, `name`, `size`, `type`, `subtype`, `alignment`
- Combat: `ac`, `hp`, `hit_dice`, `speed`
- Abilities: `stats` in STR, DEX, CON, INT, WIS, CHA order
- Proficiencies: `saves` and `skillsaves` lists of ability/skill-to-modifier mappings
- Information: `senses`, `languages`, `cr`
- Defenses: `damage_vulnerabilities`, `damage_resistances`, `damage_immunities`, `condition_immunities`
- Sections: `traits`, `actions`, `bonus_actions`, `reactions`, `legendary_actions`, `spells`

Traits, actions, bonus actions, reactions, and legendary actions use this structure:

```json
"traits": [
  {
    "name": "Trait Name",
    "desc": "Trait description.",
    "attack_bonus": 0
  }
],
"actions": [
  {
    "name": "Action Name",
    "desc": "Action description.",
    "attack_bonus": 0
  }
]
```

For attacks, use numeric `attack_bonus`, and add `damage_dice` and `damage_bonus` only when applicable. Keep the complete attack text in `desc`; do not invent unsupported JSON fields. Spell entries are strings in a list.

## Personal Preferences

- Always prefix custom-created monster names with `HB` (for example, `HB Half-Blood Vampire`). Keep the same prefixed name in the JSON key, creature object's `name`, and Markdown `monster` reference.
- Write statblocks compactly. Include mechanics players or the DM need to run the creature, but leave out unnecessary detail and rules text that is already obvious or implied. For example, do not add phrases such as "requiring no material components" unless that fact matters for play.
- When mentioning spells, do not write spell descriptions in the statblock. Use the spell name and only the necessary casting or gameplay details. When the `dnd-wiki-obsidian` skill is available, add the mentioned spells after the statblock as DnD Wiki spell blocks, preferring 2024 spell entries where an equivalent exists.
- Avoid giving a creature resistance to bludgeoning, piercing, and slashing damage all at once. That combination can make melee characters less effective and less able to play around the creature's defenses. If damage resistances are appropriate, normally choose a narrower resistance or another defense so players retain meaningful counterplay.

## Existing creatures

- Use the Markdown `monster: Creature Name` reference when recalling a bestiary or custom creature.
- Combine `monster` with explicit fields to override values.
- Use `extends` for a variant based on one or more creatures.
- Use `actions+`, `actions-`, or equivalent list operators only when adding to or removing from inherited lists.
- When editing an existing custom creature, make the smallest targeted change to its JSON entry and keep the Markdown note as a reference.

## JSON and Reference Validation

Before returning a block, verify:

1. The JSON remains valid.
2. Only the intended entry or entries in `monsters` changed; unrelated monsters and top-level settings remain unchanged.
3. The creature's key, object `name`, and Markdown `monster` reference match exactly.
4. `stats` contains six values in standard ability-score order.
5. `cr` uses the plugin's expected string format.
6. Every trait/action entry has `name`, `desc`, and the expected numeric attack fields where applicable.
7. The Markdown reference uses exactly the `statblock` fence and includes `monster`.

## Missing information

Do not invent important statistics unless the user asks you to design the creature. Ask for missing information when needed; if designing it, state the assumptions briefly outside the code block.

Troubleshoot the JSON entry and reference first: valid JSON, `monsters` entry shape, matching names, supported fields, numeric types, and the Markdown reference fence.

## Final Reload Step

- After all statblock JSON and Markdown edits are complete and verified, run this as the **very last tool action**:

  ```text
  obsidian vault="Vault Name" reload
  ```

- Replace `Vault Name` with the actual vault name. Do not run this command before all edits and checks are finished; reloading the vault can interrupt or cancel the agent before it reports completion.
- This final step is required because the custom `data.json` file was edited manually and the running plugin may still be using its old in-memory data. Reload the **vault**, not just the plugin.
- If the user reports that the command did not work, tell them to enable **Settings → General → Command line interface** in Obsidian, then retry the final command.
