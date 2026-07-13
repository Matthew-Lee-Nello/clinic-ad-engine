---
name: client-core
description: Stage 1 of the research engine. Understand the client to the core by ingesting their Google Drive folder (doctor media + onboarding) plus any intake, into a structured client profile. Trigger with "/client-core", "understand this client", "read the client's drive folder".
---

# client-core

Understand the client to the core. This is where the whole brief starts. Output to `clients/<slug>/00-brief.md` section 1 (create the brief from `templates/market-strategy-brief.md` if it does not exist).

## Ingest the client's Drive folder

Daniel keeps a per-client Google Drive folder: doctor images, videos, onboarding notes, point-of-difference material. Read it, in order of what is available:

1. **Composio** (Daniel has it). Use Composio's Google Drive tools to list the client's folder and pull the docs and notes; note the media files (images, videos) by name and type. Confirm the connection first; if Google Drive is not connected in Composio, say so and fall back.
2. **Local folder** fallback: if a local path to the synced Drive folder is given in the intake, read it directly.
3. **Pasted links** fallback: fetch shared Drive doc links via Exa/crawl.

Never guess the folder contents. If you cannot access it, say exactly which method failed and ask for a local path or a Composio connection.

## Build the profile

From the folder plus `clients/<slug>/intake.md` (if present), extract into brief section 1:
- Doctor and clinic, credentials, HCSA licence status.
- The doctor's real, substantiable point of difference (technique, technology, training, process). No marketing gloss, no unsubstantiated claim.
- Strengths to lead with.
- What the client wants to market and why now.
- Assets on hand (which doctor media/footage exist, so later stages know what can be produced).
- Country, language, funnel.

## Rules

- Only record what the folder or the client actually supports. If the point of difference is unclear, flag it as the single most important gap to fill on the onboarding call, do not invent one.
- This profile feeds every later stage. Get the point of difference right above all else.
- Write section 1 of the brief and stop; the orchestrator moves to `treatment-research`.
