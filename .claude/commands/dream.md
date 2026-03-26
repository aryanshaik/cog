Use this skill for nightly graph reasoning and new-insight generation. Trigger if the user says "dream", "nightly synthesis", "connect all sessions", or similar.

## Domain

Cross-memory synthesis using the full graph: session notes + canonical memory files.

## Inputs

1. Latest session notes in `memory/sessions/YYYY-MM-DD/*.md` (Obsidian format)
2. High-importance memory files across domains
3. `memory/cog-meta/patterns.md`
4. `memory/link-index.md`

## Process

1. Load recent session notes (last 24h by default).
2. Traverse linked files via `[[wiki-links]]` to identify cross-domain intersections.
3. Run hypothesis generation:
   - repeated motif across sessions,
   - latent conflict between priorities,
   - opportunity where one action unlocks 2+ domains.
4. For each insight, include confidence and explicit source links.
5. Update importance scores for files that were central to high-value insights.

## Output

Write one nightly file:
- `memory/cog-meta/dreams/YYYY-MM-DD.md`

Template:

```markdown
<!-- L0: Nightly cross-graph synthesis and emergent insights -->
<!-- importance: 0.55 -->
<!-- updated: YYYY-MM-DD -->
# Dream Synthesis — YYYY-MM-DD

## Insight Candidates
- [confidence: high|med|low] <insight>
  - Why it matters: <impact>
  - Sources: [[file-a]], [[file-b]], [[file-c]]

## Proposed Experiments
- [ ] <small test to validate an insight>

## Reinforcement Actions
- <file> importance: <old> → <new> (reason)
```

## Rules

- Keep outputs plain markdown and Obsidian-compatible.
- Do not invent facts; every claim must cite source links.
- Produce insights, not summaries.
- One dream file per night (append sections if rerun same date).
