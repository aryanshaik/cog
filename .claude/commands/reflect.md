Use this skill for self-reflection and continuous memory scoring. Trigger if the user says "reflect", "what have you learned", "how can you improve", "review yourself", or similar introspection requests.

## Domain

Self-improvement, memory quality, and importance-score maintenance.

## Continuous Memory Scoring Model

Every memory file is part of one shared pool and should include:

- `<!-- L0: ... -->`
- `<!-- importance: 0.00 -->` (0.00–1.00)
- `<!-- updated: YYYY-MM-DD -->`

### Score dynamics

- **Decay (idle files):** reduce score by ~2% per day since `updated`
- **Reinforcement (used files):** increase score when a file is mentioned, read, edited, or cited
  - light mention: `+0.03`
  - strong relevance / direct update: `+0.07`
  - critical decision anchor: `+0.10`
- Clamp all scores to `[0.00, 1.00]`
- Keep a floor of `0.05` unless the user explicitly asks to suppress a file

### Manual boost

Allow explicit boosts during reflect:

- `boost [[path/to/file]] by 0.10`

Apply boost immediately, clamp to 1.00, and note it in the debrief.

## Process

1. Read recent sessions from `memory/cog-meta/reflect-cursor.md` scope.
2. Export each newly processed session as an Obsidian note in `memory/sessions/YYYY-MM-DD/session-<HHMMSS>.md`.
3. Identify files/facts actively used, repeated, or newly important.
4. Apply reinforcement to those files.
5. Apply decay to files not touched recently.
6. Update `updated` dates for modified files.
7. Keep files in place (no tier moves, no archival routing).
8. Debrief with: files updated, old score → new score, and why.

## Rules

- Do not use hot/warm/glacier language.
- Do not move files to cold storage as part of reflection.
- Preserve plain-text markdown and Unix tool friendliness.
- Session exports must be Obsidian-compatible markdown with frontmatter and `[[wiki-links]]`.
