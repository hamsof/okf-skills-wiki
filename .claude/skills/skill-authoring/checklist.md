---
type: reference
title: Pre-commit checklist
tags: [checklist, gate, review, validation, site]
timestamp: 2026-11-10T00:00:00Z
---

# Pre-commit checklist

Manual gate. Run through this before committing any skill change. Renderer rules:
[site-rendering.md](site-rendering.md).

## Frontmatter

- [ ] Every `.md` touched (index **and** leaf) has a YAML frontmatter block.
- [ ] `type` is exactly `index` or `reference`.
- [ ] `title`, `tags`, `timestamp` present on every file.
- [ ] `index` files also have `name` + a keyword-rich `description`.
- [ ] `timestamp` updated on every file you changed.
- [ ] Parser-safe: `---` on line 1, `tags: [inline, list]`, single-line unquoted values
      (see [frontmatter-spec.md](frontmatter-spec.md#parser-safe-syntax)).

## Tags

- [ ] kebab-case, lowercase.
- [ ] cover domain + subject + any cross-domain hook.
- [ ] an index's `tags` reflect the union of its children's themes.

## Structure

- [ ] One concept per leaf file.
- [ ] Each skill/sub-skill folder has its own `SKILL.md` (`type: index`).
- [ ] Folder/file names are kebab-case; slug matches folder name.

## Index table

- [ ] Every new/changed leaf appears in its folder's index table with tags.
- [ ] No orphan leaves — each reachable from an index.

## Cross-links

- [ ] Cross-domain dependencies linked **both ways**.
- [ ] All links use relative paths and resolve.
- [ ] Doc links are inline `[x](path.md)` with no spaces, so they become graph edges.
- [ ] No duplicated content — link to the canonical doc instead.
