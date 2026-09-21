---
name: image-generation
description: Generate D&D and general-purpose images while maintaining visual consistency across separate chats. Before generating, search existing image metadata for related factions, characters, locations, cultures, organizations, creatures, objects, or other named entities.
---

# Image Generation

Generate images and use previously generated images and their metadata as visual memory.

The workflow must support D&D campaign concepts while remaining generic enough for any type of image.

## Vault Root

Treat the directory containing `.agents` as the root of the Obsidian vault.

## Output Location

Save generated images in the `_img` folder at the root of the Obsidian vault:

```text
<vault-root>/_img/
```

Do not create subfolders by default.

Only use a subfolder when the user request it, or it makes sense to organize images by category:

```text
<vault-root>/_img/<subfolder>/
```

Never store generated images or image metadata inside the skill folder.

## Image Metadata

Every generated image must have a Markdown metadata file beside it.

Use the same base filename followed by `.image.md`:

```text
_img/golden-sun-soldier.png
_img/golden-sun-soldier.image.md
```

Create the metadata file immediately after generating the image.

## Before Generating an Image

1. Determine the Obsidian vault root.
2. Identify named associations in the request.
3. Search `_img` and all its subfolders for existing `*.image.md` files with matching associations.
4. Read all relevant matching metadata files.
5. Inspect the associated images when the image-generation tool supports image references.
6. Extract reusable visual details.
7. Incorporate those details into the new image prompt.
8. Generate the image.
9. Save the image and its metadata sidecar.

Associations may include:

- Characters
- Factions
- Kingdoms
- Religions
- Cultures
- Organizations
- Creatures
- Species
- Locations
- Objects
- Items
- Events
- Other recurring named concepts

Normalize association IDs using lowercase letters and hyphens:

```text
Golden Sun → golden-sun
Kingdom of Ash → kingdom-of-ash
Sir Aldric → sir-aldric
```

Prefer metadata matches in this order:

1. The same character, creature, location, or object.
2. The same faction, kingdom, religion, culture, or organization.
3. Other explicitly related entities.

Do not use generic concepts such as `soldier`, `priest`, or `city` to make unrelated images visually similar.

Continuity should primarily come from named associations such as `golden-sun`.

## Using Existing Metadata

If relevant metadata exists, reuse its visual identity.

For example:

1. An image of a Golden Sun soldier already exists.
2. Its metadata contains the `golden-sun` association.
3. The user requests a Golden Sun priest in a new chat.
4. Search for `golden-sun`.
5. Read the soldier’s metadata and inspect the image when possible.
6. Reuse the Golden Sun colors, symbols, materials, and design language.
7. Do not copy the soldier’s weapon, pose, armor, or battlefield setting unless relevant.

If no matching metadata exists, create an appropriate new visual identity and record it for future generations.

## Classifying Visual Details

A detail belongs under `Reusable Visual Identity` when it should influence another image connected to the same association.

Examples include:

- Colors and palettes
- Heraldry
- Religious symbols
- Materials
- Patterns and motifs
- Cultural design language
- Clothing styles
- Armor styles
- Architectural styles
- Recurring physical features of a character or creature
- Overall artistic direction

A detail belongs under `Image-Specific Details` when it only applies to the current image.

Examples include:

- Pose
- Facial expression
- Current action
- Weather
- Time of day
- Background composition
- Scene-specific lighting
- Equipment unique to the depicted role
- Damage, dirt, or temporary conditions

Use this test:

> Should this detail also appear in a different image connected to the same association?

If yes, record it as reusable visual identity.

If no, record it as image-specific.

## Metadata Format

Use [references/metadata-template.md](references/metadata-template.md) when creating sidecar metadata. Never copy example values into generated metadata.
Use this structure for every `.image.md` sidecar:

---
schema_version: 1
image: golden-sun-priest.png
title: Golden Sun Priest
created: 2026-09-21
associations:
  - id: golden-sun
    name: Golden Sun
    type: faction
references_used:
  - _img/golden-sun-soldier.image.md
generation:
  provider: OpenAI
  model:
  model_version:
  quality: high
  size: 1024x1536
  width: 1024
  height: 1536
  aspect_ratio: "2:3"
  format: png
  background: opaque
  seed:
  settings: {}
---

## Original Request

Make an image of a priest of the Golden Sun.

## Final Prompt

A full-body fantasy priest belonging to the Golden Sun faction. The priest wears white and gold ceremonial robes decorated with the faction’s radiant sun emblem. Polished brass details and warm golden materials match the established appearance of the Golden Sun soldier. The priest carries a ceremonial staff and stands inside a sunlit temple.

## Reusable Visual Identity

- Colors: White, gold, and warm yellow
- Symbols and heraldry: Radiant golden sun
- Materials: Polished brass, white cloth, and gold embroidery
- Patterns and motifs: Sun rays and circular designs
- Design language: Bright, ceremonial, disciplined, and religious
- Overall aesthetic: Noble followers of a solar faith

## Inherited Continuity

The white-and-gold palette, radiant sun emblem, polished brass, and disciplined appearance were inherited from `golden-sun-soldier.image.md`.

## Image-Specific Details

- Ceremonial priest robes
- Religious staff
- Sunlit temple interior
- Calm standing pose

## Generation Notes

The military visual identity of the Golden Sun was adapted into a religious role while preserving the faction’s established colors, symbols, and materials.

## Metadata Rules

- Preserve the original request separately from the final prompt.
- Record all genuinely relevant named associations.
- Record metadata files and images used for continuity in `references_used`.
- Use normalized association IDs consistently.
- Describe reusable identity clearly enough for a future AI to apply it.
- Keep image-specific details separate from reusable identity.
- Keep generation notes concise and useful.
- Do not store hidden chain-of-thought.
- Do not invent campaign lore merely to fill metadata fields.
- Keep the image and its metadata file in the same directory.
- If the image is placed in a user-requested subfolder, place its metadata there as well.

## After Generation

1. Confirm that the image was saved under `<vault-root>/_img/` or an explicitly requested subfolder.
2. Create the matching `.image.md` file.
3. Verify that the metadata references the correct image filename.
4. Verify that association IDs are normalized.
5. Verify that all available model, quality, size, and technical settings were recorded accurately.
6. Report the image path and metadata path to the user.