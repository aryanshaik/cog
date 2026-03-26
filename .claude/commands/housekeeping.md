Use this skill to perform continuous memory housekeeping. Trigger if the user says "housekeeping", "clean up memory", "prune memory", or similar maintenance requests.

## Model

Memory is a continuous spectrum, not discrete tiers. All files stay in their existing domain paths and are ranked by `importance` metadata.

Required per markdown memory file:
- `<!-- L0: ... -->`
- `<!-- importance: 0.00 -->`
- `<!-- updated: YYYY-MM-DD -->`

## 1) Recalculate Importance Globally

For all memory files:
1. Read current `importance` and `updated`.
2. Apply time decay (default: 2% relative per idle day).
3. Apply reinforcement signals from recent references (reflect outputs, new edits, active links).
4. Clamp to `[0.00, 1.00]`.

## 2) Keep Everything In Place

- No archival moves.
- No glacier index rebuilds.
- Low-importance files remain in place and searchable; they are just rarely loaded.

## 3) Prune Only Ultra-Low Signal

Prune content only when all are true:
- importance is below a very low threshold (default `<0.03`),
- the content is duplicated elsewhere (SSOT violation), and
- no explicit user pin/boost exists.

If pruned, retain a short pointer to canonical source instead of deleting context silently.

## 4) Initial-Load Set Refresh

Generate/refresh a top-load list by score:
- top N files globally or
- all files above threshold (e.g., `>=0.35`).

This list controls what is loaded first at session start.

## 5) Nightly Dream Trigger

At night (or scheduled daily close), trigger `/dream` to perform graph-wide reasoning:
- consume recent session notes from `memory/sessions/`,
- connect them with existing memory files via `[[links]]`,
- write new insight hypotheses to `memory/cog-meta/dreams/YYYY-MM-DD.md`,
- reinforce files used in high-value cross-domain connections.

## 6) Debrief

Report:
- files rescored,
- largest positive/negative score changes,
- any ultra-low-signal pruning,
- updated top-load set,
- whether nightly `/dream` ran and where output was written.
