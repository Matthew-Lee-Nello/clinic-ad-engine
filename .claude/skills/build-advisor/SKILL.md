---
name: build-advisor
description: Build or refresh a persona advisor's corpus from source, portable with no gbrain/Ollama. Scrapes a YouTube channel (Apify) or converts a book (pdftotext) into plain markdown, then distils the always-read primer. Trigger with "/build-advisor <name>", "build the mark corpus", "refresh the schwartz advisor".
---

# build-advisor

Populate a persona advisor's `knowledge/<persona>/` folder and distil its `_<persona>-primer.md`. Fully portable: yt-dlp or Apify, pdftotext, and the agent itself for distillation. No gbrain, no Ollama, no embeddings.

Currently the corpus that needs building on a fresh clone is **mark** (Mark Builds Brands). Hormozi and Schwartz ship pre-built.

## For a YouTube persona (e.g. mark)

Source: the channel URL in `knowledge/<persona>/README.md`.

1. **Enumerate videos.** Preferred: `yt-dlp --flat-playlist --print "%(id)s|%(title)s" "<channel>/videos"` to a temp file. If yt-dlp is not installed or is network-blocked, use an Apify channel-scraper actor to list video URLs.
2. **Transcribe in batch** with the Apify actor `karamelo/youtube-transcripts` via `mcp__apify__call-actor`:
   - `fetch-actor-details` for the input schema.
   - Call with `urls` = the video URLs, `outputFormat: "singleStringText"`. Needs `APIFY_TOKEN`.
   - Pull results with `mcp__apify__get-dataset-items` (or the dataset REST endpoint).
   - ~$0.007/video, batch-native. Free fallback if available: `youtube_transcript_api`.
3. **Write one markdown file per video** into `knowledge/<persona>/`, named `<persona>-<VIDEO_ID>.md`, each with frontmatter (`title`, `url`, `video_id`, `channel`, `fetched_at`) then the transcript body. Skip videos already present (idempotent). Log failures in `_failed.md`.
4. **Distil the primer.** Read the whole corpus and rewrite `_<persona>-primer.md`: the creator's philosophy, repeated frameworks, formats, hooks, and voice, in the same shape as `knowledge/hormozi/_hormozi-primer.md`. Keep it tight (one page), it is read every call.

## For a book persona (e.g. schwartz, already shipped)

1. `pdftotext -layout -nopgbrk "<book.pdf>" knowledge/<persona>/<book-slug>.md`.
2. Check the output has real text (word count > 1000; if not, the PDF is scanned and needs OCR).
3. Distil `_<persona>-primer.md` from the book.

## Optional graph layer (Daniel's call, not required)

After a corpus is built, from the repo root:
- `graphify .` builds `graphify-out/` for cross-document navigation (portable; no API key, uses the host Claude session as the LLM; needs the `graphify` python install).
- A wikilink pass across `knowledge/` can cross-link related concepts between personas. Nice for navigation, never required for the advisors to work.

## Rules

- Portable first: never introduce a gbrain, Ollama, or embedding dependency. The advisors read plain markdown.
- Idempotent: re-running skips what already exists and only fills gaps.
- Never fabricate transcript content. If a video will not transcribe, log it and move on.
