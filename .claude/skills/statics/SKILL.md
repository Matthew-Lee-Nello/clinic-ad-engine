---
name: statics
description: Generate static ad images for the angles that suit a static, using the image model (gpt-image). Compliant with the clinic's jurisdiction - no before/after imagery, no results depiction, no superlative text baked into the image. Trigger with "/statics", "generate the statics", "make the ad images".
---

# statics

Generate one static image per angle marked static or both in `clients/<slug>/02-angles.md`. Save to `clients/<slug>/statics/`. Read `03-copy.md` and `knowledge/singapore-ad-compliance.md` first.

## Compliance for images (strict)

- **No before-and-after. No after-only depiction** of a treatment result on a face or body.
- **No implied results** (no "flawless skin" transformation imagery presented as an outcome).
- **No superlatives or laudatory claims** in any text baked into the image (no "best", "No.1", "guaranteed").
- **No testimonial** text or star ratings.
- Any on-image text must be factual and pass the compliance gate.
- Prefer clean, editorial, educational visuals: the clinic environment, the doctor, the mechanism illustrated, informational layouts, tasteful brand-led design. Not sensational.

## Generation

Use the image model (gpt-image). Two common paths, use whichever is wired in this environment:

- If the `codex-image` skill or an image MCP is available, call it with the prompt.
- Otherwise call the OpenAI image API (gpt-image-1) via a small script using `OPENAI_API_KEY`, writing the PNG to `clients/<slug>/statics/`.

For each static:
1. Build a prompt from the angle's core idea plus the clinic's brand cues (colours, tone from the intake), constrained by the image-compliance rules above.
2. Generate at a Meta-friendly ratio (1:1 `1024x1024` for feed, or 4:5 for mobile).
3. Save as `clients/<slug>/statics/NN-<angle-slug>.png`, NN matching the angle number.
4. Record the prompt used alongside, so a static can be regenerated or tweaked.

## Output

- One PNG per static angle in `clients/<slug>/statics/`.
- A `statics/manifest.md` listing each file, its angle number, the prompt, and a compliance-clear tick.

If any generated image drifts toward a results depiction or bakes in a non-compliant claim, discard and regenerate with a tighter prompt. Never ship a non-compliant static.
