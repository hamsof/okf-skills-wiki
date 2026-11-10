---
type: reference
title: Cross-linking & the knowledge graph
tags: [links, graph, see-also, nested, cross-folder, discovery, site]
timestamp: 2026-11-10T00:00:00Z
---

# Cross-linking & the knowledge graph

This is the part that solves nested-skill discovery. OKF docs link to each other via
markdown links, forming a graph. The model follows links — including links into *other*
skill folders — so deeply-nested knowledge reaches it without you naming the nested skill.

## Link styles

| Scope | Form | Example |
|-------|------|---------|
| Within a folder | relative file | `[checkout.md](checkout.md)` |
| Into a child folder | relative path down | `[setup](server/setup.md)` |
| Into a sibling skill | relative path up+over | `[Sale by Product](../reports/sales-by-product.md)` |

Always use **relative paths** so links survive being moved, mirrored, or rendered to HTML.

## Links that count as graph edges

The wiki renderer builds its D3 graph only from links matching `](path.md)` or
`](path.md#anchor)` (see [site-rendering.md](site-rendering.md)). So:

- Use **inline** markdown links. Reference-style `[x][ref]`, bare paths in prose and
  paths in backticks are not edges.
- No spaces or `)` in link paths. Keep files kebab-case.
- A link to a file that doesn't exist, or that resolves outside the bundle root, is
  dropped from the graph. On the page it still turns into a broken `.html` link.
- Self-links are ignored, and the same edge is counted once per source doc.
- Every `.md` href is rewritten to `.html`. External URLs are left alone, so link to code
  or GitHub with a full URL rather than a repo-relative `.ts` path.

## The both-ways rule

> If knowledge in folder A is needed while reading folder B, link both ways.

Example: the reports depend on the checkout invoice shape. So
`reports/sales-by-product.md` links to `../pos-flow/checkout.md`, and
`pos-flow/checkout.md` links back to the reports. Arriving from either side, the model can
pull the other.

## `See also` block

End a leaf with an explicit block when it has cross-domain dependencies:

```markdown
## See also
- [../pos-flow/checkout.md](../pos-flow/checkout.md) — where the Invoice shape is built
```

## What this does NOT change

It does not change an agent host's autocomplete. Discovery moves into the model: it reads
an index, matches `tags`, and walks links across folders. The graph is the search index;
the model is the search engine. A static site builder can walk the same links to produce a
browsable HTML version of the graph.
