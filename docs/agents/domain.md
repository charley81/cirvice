# Domain Docs

Before exploring the codebase, read:

- `GLOSSARY.md` at the repository root, when present.
- Relevant ADRs under `docs/adr/`.

If these files do not exist, proceed silently. Domain-modeling skills create
them when terminology or decisions are actually resolved.

This is a single-context repository:

```
/
├── GLOSSARY.md
├── docs/adr/
└── src/
```

Use terms as defined in `GLOSSARY.md`. Do not drift to synonyms the glossary
explicitly avoids.

If proposed work contradicts an existing ADR, identify the conflict explicitly
rather than silently overriding the decision.
