# Mark Builds Brands corpus (populate this)

This folder is empty on purpose. It gets filled by Daniel's agent, not shipped pre-built, because scraping is the expensive step.

Source: YouTube channel `https://www.youtube.com/@markbuildsbrands` (the creator Daniel models for creative and brand style).

## To build it

Run `/build-advisor mark`, or paste `BOOTSTRAP.md` and let it drive. That runbook will:

1. Enumerate the channel's videos (`yt-dlp --flat-playlist`, or a channel-scraper Apify actor).
2. Transcribe them via the Apify actor `karamelo/youtube-transcripts` (token-only, ~$0.007/video, batch `urls`). Needs `APIFY_TOKEN`.
3. Write one markdown file per video into this folder, `mark-builds-brands-<VIDEO_ID>.md`, with frontmatter (title, url, video_id, date) plus the transcript.
4. Distil `_mark-primer.md` from the whole corpus: his creative philosophy, brand approach, ad formats, hooks, and any repeated frameworks, in the same shape as `../hormozi/_hormozi-primer.md`.

Optional after building: `graphify .` from the repo root, and a wikilink pass across `knowledge/`, for cross-document navigation. Not required for the advisor to work.

Until this is populated, the `advisor-mark` skill runs on `_mark-primer.md` alone and notes that the full corpus is not yet built.
