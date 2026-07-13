---
name: clinic-campaign
description: Master orchestrator for a full clinic ad campaign. Runs the whole Jeremy Haynes pipeline end to end for one treatment - market research + Meta Ads Library scrape, 25-30 compliant angles, 5 headlines + 5 body copies + video scripts, static generation, and the paused Meta campaign build. Trigger with "/clinic-campaign", "build a campaign for <treatment>", "run the full pipeline", or after an intake is filled.
---

# clinic-campaign

The master run. Orchestrates every stage for one treatment. Read `CLAUDE.md`, `knowledge/haynes-method.md`, and `knowledge/singapore-ad-compliance.md` first if not already loaded this session.

## Preconditions

- Know the client's Drive folder (via Composio) or a local path, plus the treatment and country. An `intake.md` is optional; the research engine pulls most of what it needs from the Drive folder. If the doctor's point of difference is unknown and not in the folder, ask for it first.
- Pick a `client-slug` (kebab-case, e.g. `dr-tan-rhino`). All stage outputs write to `clients/<client-slug>/`.

## Run order — research first, then a review gate, then creative

Run each stage, writing its output to disk before the next reads it. Do not hold the whole run in memory.

### Phase A - research (the core)

Run `market-research`, which runs the six research stages into one brief:
`client-core` → `treatment-research` → `market-sizing` → `competitor-swipe` → `positioning` → `strategy-brief`, all writing into **`clients/<slug>/00-brief.md`** (the Market & Strategy Brief). This is the heavy, valuable part and what makes the system repeatable across clients.

### GATE - Daniel reviews the brief

Stop. Hand `00-brief.md` to Daniel. Do NOT run any creative stage until he ticks the approval box in the brief. Research quality decides everything downstream.

### Phase B - creative + launch (only after approval)

1. **angles** -> `clients/<slug>/02-angles.md`
   25 to 30 distinct, compliant reasons to convert, generated FROM the approved brief (angle territory, swiped concepts, positioning), consulting the Schwartz/Hormozi/Mark advisors. Each passes compliance. Log dropped angles.

2. **scripts-and-copy** -> `clients/<slug>/03-copy.md`
   The shared pool of 5 headlines and 5 body copies (through the Schwartz copywriter + a Hormozi hook pass), plus a short video script per angle. All compliant.

3. **statics** -> `clients/<slug>/statics/`
   Generate the static ad images for the angles that suit a static (Mark advisor for direction). Filename maps to the angle.

4. **launch** -> `clients/<slug>/04-launch-plan.md` then the paused build
   Build the campaign in Meta, paused. Three ad sets (broad, interest stack, lookalike stack), the same ads and 5+5 copy in each, ABO budgets, auto-features off. Show the plan and get a yes before anything goes live.

## After the run

Write a one-page summary to `clients/<slug>/README.md`: what was produced, the compliance items dropped, the launch structure, and the exact next actions for the human (film the video angles, review the paused campaign, set it live). Then report to the user what you built and where it landed.

## Rules

- Compliance is checked at each stage, not at the end. A non-compliant angle never reaches copy or statics.
- Never fabricate a claim, a statistic, or a testimonial.
- Never set a campaign live without an explicit yes from the human.
