---
name: strategy-brief
description: Stage 6 of the research engine. Synthesise the whole research into the concrete game plan - the highest-probability play for this treatment - and finalise the Market & Strategy Brief for Daniel's review. Trigger with "/strategy-brief", "give me the game plan", "finalise the brief".
---

# strategy-brief

Turn the research into a decision. Output to brief section 6 and finalise `clients/<slug>/00-brief.md`. Read sections 1-5 first.

## Do this

Synthesise everything into the game plan:

- **Angle territory:** the themes the 25-30 angles will be built from, drawn from the real market questions (section 2), the swiped concepts (section 4), and the positioning wedge (section 5). This is the handoff to the `angles` stage. Do not write the 25-30 here, just the territory and why.
- **Recommended structure:** starting budget read, ad-set setup (per `knowledge/haynes-method.md`), and what to test first given the market and budget.
- **The reasoning:** why this plan gives THIS treatment the most probable chance of working. Daniel does not want guaranteed ROAS, he wants the highest-probability play, argued.
- **Open risks + what would change the plan** (e.g. TAM says budget is the constraint, or the POD is unclear).

## Finalise + gate

- Fill section 6, then read the whole brief top to bottom and tighten it into one coherent document.
- Set the status to "DRAFT for review" and leave the approval checkbox unticked.
- **Stop here and hand the brief to Daniel.** Research quality decides everything downstream, so nothing creative runs until he approves. Tell him the brief is ready at `clients/<slug>/00-brief.md` and summarise the game plan in three lines.

## Rules

- The plan must trace back to the research; no recommendation without a reason from sections 1-5.
- Compliant throughout. Do not start `angles` until the brief is approved.
