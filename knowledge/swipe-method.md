# Swipe method (read a winning ad anywhere, adapt the concept, compliantly)

Swiping is a core part of the research, and it works cross-market: the best concept for a Singapore treatment may be running in a completely different country or niche. You do not copy the ad. You extract the transferable *idea* and rebuild it as your own, inside the compliance rail.

Danny's own words: "it can be a different market, the concept you can swipe." And: read the ad or watch the video, extract the transcript, and make it ours.

## What a "winner" is

You cannot see conversions from outside, so use proxy signals, strongest first:
- **Longevity:** the ad has been running a long time (Meta Ad Library shows the start date). Advertisers kill losers fast, so a long-running ad is usually paying its way.
- **Volume:** the same advertiser runs many variations of the same concept.
- **Repetition across advertisers:** several serious players converge on the same concept.
- Danny's known reference: Mark Builds Brands (low CPL, good lead quality) — a known-good source to study.

State the signal you used. Never claim an ad "converts" from outside data.

## How to read an ad

**Static (image) ad** — read it with vision:
- The hook (first thing the eye lands on), the core promise or idea, the visual device, the structure (problem/solution, question, list, comparison), the call to action.

**Video ad** — extract the transcript, then read structure:
- The first 3 seconds (the stop), the narrative arc, the mechanism explained, the proof device, the close. Transcribe via the Apify actor `karamelo/youtube-transcripts` for YouTube, or the ad's own captions/audio where available.

Capture the **concept**, not the wording: "explain the hidden cause of the problem before offering the fix", "day-in-the-life of the condition", "myth vs fact", "the doctor walks you through the process". Concepts travel across markets; specific copy does not.

## How to adapt (the swipe → brief)

For each winner worth swiping, output an adaptation brief:
- **Source:** where it ran, the market/niche, the longevity signal.
- **The concept:** the transferable idea in one line.
- **Why it works:** the psychology (which awareness stage, which desire).
- **Our version:** how it maps to this treatment + the doctor's point of difference.
- **Compliance pass:** rewritten to clear `singapore-ad-compliance.md` — strip any before/after, testimonial, superlative, results claim, or soliciting. If the concept *depends* on a banned device (e.g. before/after transformation), say so and either adapt it to a compliant form or drop it.

## Hard rails

- Never lift copy or creative wholesale. Swipe the concept, rebuild it as ours.
- Never carry a competitor's non-compliant move into our ad just because it is running.
- Never fabricate that an ad exists or that it "won". If the library is thin for the niche, swipe from adjacent markets and say that is what you did.
- Compliance always wins over a clever swipe.

## Output (feeds the brief and the angles)

A ranked list of swiped concepts with adaptation briefs, tagged by which treatment angle territory they serve. `competitor-swipe` writes these into the research brief; `angles` draws on them as raw material for the 25–30, never as finished ads.
