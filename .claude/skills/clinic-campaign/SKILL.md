---
name: clinic-campaign
description: Master orchestrator for a full clinic ad campaign. Runs the whole Jeremy Haynes pipeline end to end for one treatment - market research + Meta Ads Library scrape, 25-30 compliant angles, 5 headlines + 5 body copies + video scripts, static generation, and the paused Meta campaign build. Trigger with "/clinic-campaign", "build a campaign for <treatment>", "run the full pipeline", or after an intake is filled.
---

# clinic-campaign

The master run. Orchestrates every stage for one treatment. Read `CLAUDE.md`, `knowledge/haynes-method.md`, and `knowledge/singapore-ad-compliance.md` first if not already loaded this session.

## Preconditions

- An intake exists at `clients/<client-slug>/intake.md`. If not, copy `templates/intake.md` there and ask the user to fill the doctor's point of difference and the target country at minimum.
- Pick a `client-slug` (kebab-case, e.g. `dr-tan-rhino`). All stage outputs write to `clients/<client-slug>/`.

## Run order

Run each stage, writing its output to disk before the next reads it. Do not hold the whole run in memory.

1. **market-research** -> `clients/<slug>/01-research.md`
   Buyer-spectrum read for the treatment in the country, plus a Meta Ads Library scrape of what competitors are running and for how long. Structure inspiration only, never a source of angles to copy.

2. **angles** -> `clients/<slug>/02-angles.md`
   25 to 30 distinct, compliant reasons to convert, spread across the buyer spectrum and anchored to the doctor's real point of difference. Each angle passes the compliance check before it is kept. Log dropped angles and why.

3. **scripts-and-copy** -> `clients/<slug>/03-copy.md`
   The shared pool of 5 headlines and 5 body copies, plus a short video script per angle for the doctor to film. All compliant.

4. **statics** -> `clients/<slug>/statics/`
   Generate the static ad images for the angles that suit a static. Save each with a filename that maps to its angle.

5. **launch** -> `clients/<slug>/04-launch-plan.md` then the live build
   Build the campaign structure in Meta, paused. Three ad sets (broad, interest stack, lookalike stack), the same ads and 5+5 copy in each, ABO budgets, auto-features off. Show the full plan and get a yes before anything goes live.

## After the run

Write a one-page summary to `clients/<slug>/README.md`: what was produced, the compliance items dropped, the launch structure, and the exact next actions for the human (film the video angles, review the paused campaign, set it live). Then report to the user what you built and where it landed.

## Rules

- Compliance is checked at each stage, not at the end. A non-compliant angle never reaches copy or statics.
- Never fabricate a claim, a statistic, or a testimonial.
- Never set a campaign live without an explicit yes from the human.
