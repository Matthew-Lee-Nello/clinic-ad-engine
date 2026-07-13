---
name: market-research
description: Entry point to the research engine. Runs the full research pipeline (client-core, treatment-research, market-sizing, competitor-swipe, positioning, strategy-brief) into one Market & Strategy Brief, then stops for review. Trigger with "/market-research", "research this treatment", "build the strategy brief".
---

# market-research (the research engine entry point)

Research is the core of this system and the thing that makes it scale across clients: the same rigorous pipeline, the same standard brief, every treatment. This skill runs the whole pipeline; the six stage skills below do the work and each writes into one brief.

If the intake or Drive folder is thin, ask for the client's Drive folder (via Composio) or a local path and the doctor's point of difference before starting.

## Run the stages in order

Create `clients/<slug>/00-brief.md` from `templates/market-strategy-brief.md`, then run each stage, which fills its section:

1. **client-core** - ingest the client's Drive folder + intake → the client profile (section 1). Point of difference above all.
2. **treatment-research** - the treatment, the patient journey, real questions and objections, country nuances (section 2).
3. **market-sizing** - TAM / SAM / SOM per `knowledge/tam-methodology.md`, with the bottom-up cross-check (section 3).
4. **competitor-swipe** - Meta Ad Library scan + cross-market swiped concepts per `knowledge/swipe-method.md` (section 4).
5. **positioning** - market gaps × the doctor's leverage = the wedge, plus the buyer-spectrum diagnosis (section 5).
6. **strategy-brief** - synthesise into the game plan and finalise the brief (section 6).

## Then stop for the gate

Hand `00-brief.md` to Daniel for review. Nothing creative runs until he approves it (the approval checkbox in the brief). Research quality decides everything downstream.

## Rules

- Never fabricate a figure, a market question, or an ad. Source or label every claim.
- Compliance rail applies to everything that will become an ad (`knowledge/singapore-ad-compliance.md`).
- Portable: plain markdown, web research, Apify, Composio for Drive. No gbrain, no embeddings.
