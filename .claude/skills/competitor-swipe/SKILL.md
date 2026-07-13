---
name: competitor-swipe
description: Stage 4 of the research engine. Scan the Meta Ad Library for competitors AND swipe winning ad concepts from any market (read the image or the video transcript, adapt the concept compliantly). Trigger with "/competitor-swipe", "scan the ad library", "swipe winning ads for this treatment".
---

# competitor-swipe

Two jobs: map who is advertising, and harvest winning concepts to adapt. Output to brief section 4. Read `knowledge/swipe-method.md` and `knowledge/singapore-ad-compliance.md` first, plus brief sections 1-3.

## Job 1: competitor scan (niche + country)

Meta Ad Library via Apify (actor for Facebook Ads Library; `search-actors` then `fetch-actor-details` then `call-actor`, needs `APIFY_TOKEN`). For each advertiser found: page name, ad longevity (start date), media type, the angle, and whether that angle would be compliant here. Fallback: the Ad Library website directly, or Crawl4AI on a known URL. If the niche/country library is thin (common in restricted markets), say so plainly.

## Job 2: swipe winning concepts (cross-market - this is what Daniel wants)

Per `knowledge/swipe-method.md`. Winners are found by proxy signal (longevity, volume, cross-advertiser repetition), and they can come from ANY market or niche, not just this treatment or country. Known-good source to study: Mark Builds Brands.

For each winner worth swiping:
- **Read it.** Static: read the image with vision (hook, promise, visual device, structure, CTA). Video: extract the transcript (Apify `karamelo/youtube-transcripts` for YouTube, or captions/audio) and read the arc.
- **Extract the concept** (the transferable idea, one line), not the wording.
- **Adapt it:** map to this treatment + the doctor's point of difference, then rewrite to clear compliance (strip before/after, testimonials, superlatives, results claims, soliciting). If the concept depends on a banned device, adapt it to a compliant form or drop it.
- Tag which angle territory it feeds.

## Rules

- Swipe the concept, never lift copy or creative wholesale.
- Never carry a competitor's non-compliant move into our ad.
- Never fabricate an ad or claim one "won"; state the proxy signal used.
- Compliance always wins. Write section 4 (competitor table + ranked swiped concepts) and stop.
