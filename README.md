# Clinic Ad Engine

An AI creative strategist and media buyer for medical and aesthetic clinics, built to run inside Claude Code. It runs the whole front end of a Meta ads operation using Jeremy Haynes' current post-Andromeda method, with advertising compliance as a hard rail.

Drop this folder into Claude Code, fill an intake, and it produces market research, 25 to 30 compliant angles, the copy pool, video scripts, static ad images, and a paused, live-ready Meta campaign.

## What it does

- **Research.** Buyer-spectrum market read (awareness and sophistication) plus a Meta Ads Library scrape of what competitors run and for how long.
- **Angles.** 25 to 30 genuinely distinct reasons to convert, spread across the buyer spectrum, anchored to the doctor's real point of difference. Every angle passes a compliance gate first.
- **Copy and scripts.** One shared pool of 5 headlines and 5 body copies, plus a short video script per angle for the doctor to film.
- **Statics.** Generated static ad images, compliance-checked (no before/after, no results depiction, no superlatives).
- **Launch.** Builds the campaign in Meta, paused: one cold campaign, three ad sets (broad, interest stack, lookalike stack), the same ads and copy in each, ABO budgets, auto-features off. Never goes live without your yes.

## Grounded advisors

Three persona brains sharpen the creative, each grounded in its own markdown corpus (portable, no gbrain, no embeddings):

- **Schwartz copywriter** (`/copywriter`) - Eugene Schwartz's Breakthrough Advertising, the copy engine. Ships with the full book.
- **Hormozi** (`/ask-hormozi`) - offer, value equation, hooks, risk reversal. Ships with the corpus.
- **Mark Builds Brands** (`/ask-mark`) - creative and brand style. Build the corpus with `/build-advisor mark` (Apify scrape of the channel).

They plug into the pipeline (angles, copy, statics) and can also be queried standalone. They inform; compliance always wins.

## Method and compliance

- The method lives in `knowledge/haynes-method.md`. It is the spine: 25 to 30 unique concepts, 3 ad sets, ABO, 1 to 3 winners by design, the duplicate-and-scale loop, the lead-quality gate.
- The compliance rail lives in `knowledge/singapore-ad-compliance.md`, built from the Singapore Healthcare Services (Advertisement) Regulations 2021. For aesthetics this bans before/afters, testimonials, superlatives, and results claims, and forbids soliciting. That is exactly why a compliant creative engine is the edge. This is a working summary, not legal advice; the clinic's licensee signs off every ad.

## Setup

1. Clone this repo and open it in Claude Code.
2. Set the environment variables the MCP servers need (see `.mcp.json`):
   - `PIPEBOARD_API_TOKEN` - Meta Ads access via Pipeboard (run the meta-ads-mcp login flow to get one, or set `META_ACCESS_TOKEN` directly).
   - `APIFY_TOKEN` - Meta Ads Library scraping and the Mark Builds Brands corpus build.
   - `EXA_API_KEY` - web research.
   - `OPENAI_API_KEY` - static image generation (gpt-image).
3. Restart Claude Code so the MCP servers load.
4. **Run the bootstrap.** Paste `BOOTSTRAP.md` into Claude Code (or say "run BOOTSTRAP.md"). It checks your env, builds the Mark Builds Brands corpus, distils the primers, optionally runs graphify, and self-tests the engine on a sample intake. Idempotent, safe to re-run.

## Run

1. Copy `templates/intake.md` to `clients/<client-slug>/intake.md` and fill it. The doctor's real point of difference and the target country are the two fields that matter most.
2. Run `/clinic-campaign`. It orchestrates every stage and writes outputs into `clients/<client-slug>/`.

You can also run any stage on its own: `/market-research`, `/angles`, `/scripts-and-copy`, `/statics`, `/launch`.

## Layout

```
CLAUDE.md                     the orchestration brain (read first)
BOOTSTRAP.md                  the master prompt: builds corpora, self-tests the engine
knowledge/
  haynes-method.md            the ad method
  singapore-ad-compliance.md  the compliance rail
  hormozi/                    Hormozi corpus + primer (ships built)
  breakthrough-advertising/   Schwartz book + primer (ships built)
  mark-builds-brands/         built by /build-advisor mark (ships as a stub)
templates/intake.md           the intake form
.claude/skills/               10 skills: 6 pipeline + 3 advisors + build-advisor
clients/<slug>/               per-client intake + all stage outputs
.mcp.json                     Meta Ads, Apify, Exa wiring
```

## Non-negotiables

- Compliance is checked at every stage, not bolted on at the end. A non-compliant angle never reaches copy or statics.
- Never fabricate a claim, statistic, or testimonial.
- The doctor is on camera and signs off compliance. The engine does strategy and build.
- Campaigns build paused and never go live without an explicit yes.
