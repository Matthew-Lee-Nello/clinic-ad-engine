---
name: swipe
description: Read any winning ad (image or video, any market) and turn it into a compliant adaptation brief - the transferable concept mapped to this treatment. Reusable standalone or called by competitor-swipe. Trigger with "/swipe <ad url or ad-library query>", "swipe this ad", "what's the concept in this ad".
---

# swipe

Read one ad, or a small set, and extract concepts to adapt. Standalone version of what `competitor-swipe` does in bulk. Read `knowledge/swipe-method.md` and `knowledge/singapore-ad-compliance.md` first.

## Input

An ad URL (Meta Ad Library, a YouTube ad, an image), or an Ad Library query, or a pasted image/screenshot.

## Do this

1. **Establish the winner signal** if known: longevity, volume, cross-advertiser repetition. State it. Never claim it "converts" from outside data.
2. **Read it:**
   - Static: read the image with vision - hook, promise, visual device, structure, CTA.
   - Video: extract the transcript (Apify `karamelo/youtube-transcripts` for YouTube, or captions/audio), then read the arc (first 3 seconds, mechanism, proof, close).
3. **Extract the concept:** the transferable idea in one line (not the wording). Concepts travel across markets; copy does not.
4. **Adaptation brief:**
   - Source + market/niche + signal.
   - The concept.
   - Why it works (awareness stage, desire).
   - Our version: mapped to the treatment + the doctor's point of difference.
   - Compliance pass: rewritten to clear `knowledge/singapore-ad-compliance.md`; if it depends on a banned device, adapt or drop.
   - Which angle territory it feeds.

## Rules

- Swipe the concept, never lift copy or creative wholesale.
- Cross-market is expected and encouraged: the best concept may run in a different niche or country.
- Never fabricate an ad. Compliance always wins.
