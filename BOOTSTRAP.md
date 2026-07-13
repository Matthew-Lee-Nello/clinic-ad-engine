# BOOTSTRAP - run this once to make the engine live

Paste this whole file into Claude Code inside the `clinic-ad-engine` repo, or say "run BOOTSTRAP.md". It is self-contained and idempotent: it only builds what is missing and is safe to re-run. It never sets an ad campaign live.

---

You are setting up the Clinic Ad Engine: an AI creative strategist and media buyer for medical and aesthetic clinics. Your method is Jeremy Haynes' current approach, your copy engine is Eugene Schwartz's Breakthrough Advertising, and your hard rail is advertising compliance. Work through the steps below in order. Report a short PASS or FAIL line after each. Do not skip the compliance rail. Do not set any campaign live.

## Step 0 - Load the brain

Read, in full, before doing anything else:
- `CLAUDE.md` (the orchestration brain and rules)
- `knowledge/haynes-method.md` (the ad method)
- `knowledge/singapore-ad-compliance.md` (the hard rail)
- the three advisor primers: `knowledge/hormozi/_hormozi-primer.md`, `knowledge/breakthrough-advertising/_schwartz-primer.md`, `knowledge/mark-builds-brands/_mark-primer.md`

Confirm you understand: 25 to 30 distinct compliant concepts, 3 ad sets, ABO, 1 to 3 winners by design, the duplicate-and-scale loop, and that compliance always wins over persuasion.

## Step 1 - Environment check

Check for these environment variables and report which are set and which are missing. Do not print their values.
- `PIPEBOARD_API_TOKEN` or `META_ACCESS_TOKEN` - Meta Ads (campaign build).
- `APIFY_TOKEN` - Meta Ads Library scraping and the Mark corpus build.
- `EXA_API_KEY` - web research.
- `OPENAI_API_KEY` - static image generation.

If any are missing, list them and continue with the steps that do not need them. Do not invent keys.

## Step 2 - Advisor corpora

Two ship pre-built, one you build.

- **Hormozi:** confirm `knowledge/hormozi/` has the corpus files plus `_hormozi-primer.md`. PASS if present.
- **Schwartz:** confirm `knowledge/breakthrough-advertising/breakthrough-advertising.md` exists and has real text (word count over 1000), plus `_schwartz-primer.md`. PASS if present.
- **Mark Builds Brands:** if `knowledge/mark-builds-brands/` has only the README and the stub primer, build it now with the `build-advisor` skill: `/build-advisor mark`. This scrapes the channel via Apify (`karamelo/youtube-transcripts`, needs `APIFY_TOKEN`), writes one markdown file per video, then distils `_mark-primer.md`. Idempotent: skip videos already present. If `APIFY_TOKEN` is missing, note that Mark cannot be built yet and continue.

## Step 3 - Distil the primers

For any corpus that was just built or refreshed, rewrite its `_<persona>-primer.md` from the full corpus: the creator's frameworks, formats, hooks, and voice, one tight page, matching the shape of `knowledge/hormozi/_hormozi-primer.md`. Hormozi and Schwartz primers already ship distilled; only refresh if you materially improve them.

## Step 4 - Optional graph layer (skip if unsure)

Only if the user wants cross-document navigation and `graphify` is installed:
- Run `graphify .` from the repo root to build `graphify-out/`.
- Optionally add wikilinks across `knowledge/` between related concepts.
This is navigation only. The engine works fully without it. Skip on any doubt.

## Step 5 - Self-test the engine (dry run, nothing goes live)

Create a throwaway sample intake at `clients/_selftest/intake.md` for a plausible treatment (for example: a rhinoplasty clinic in Singapore, doctor with a named surgical technique as the point of difference). Then run the pipeline in dry mode:

1. `market-research` - produce a buyer-spectrum read (awareness and sophistication) and note the Ad Library step (a real scrape if `APIFY_TOKEN` is set, otherwise note it as skipped).
2. `angles` - generate at least 25 compliant angles, consulting Schwartz (awareness/sophistication), Hormozi (hook/offer), and Mark (style). Confirm each angle passes the compliance check, and that dropped angles are logged with reasons.
3. `scripts-and-copy` - produce the 5 headlines and 5 body copies and two sample video scripts, written through Schwartz with a Hormozi hook pass, all compliant.
4. `statics` - describe (do not necessarily generate) two static concepts, confirming they carry no before/after, no results depiction, no superlatives.
5. `launch` - produce the launch PLAN only (`clients/_selftest/04-launch-plan.md`): campaign, 3 ad sets, ABO budgets, the ad-to-angle map. Do NOT create anything in Meta during the self-test.

## Step 6 - Green/red checklist

Print a checklist with PASS or FAIL for each:
- [ ] Brain loaded (method + compliance + primers).
- [ ] Env: Meta / Apify / Exa / OpenAI (mark each set or missing).
- [ ] Hormozi corpus present.
- [ ] Schwartz corpus present (real text).
- [ ] Mark corpus built (or noted as pending on `APIFY_TOKEN`).
- [ ] Self-test produced 25+ compliant angles.
- [ ] Self-test copy passed the compliance rail.
- [ ] Launch plan generated (nothing set live).

Then delete `clients/_selftest/` and give a one-paragraph summary: what is ready, what is pending (usually the Mark corpus if the token was missing), and the exact next action for the operator (fill a real intake at `clients/<slug>/intake.md`, then run `/clinic-campaign`).

## Non-negotiables (repeat, because they matter)

- Compliance always wins. A persuasive line that breaches `knowledge/singapore-ad-compliance.md` is not usable.
- Never fabricate a claim, statistic, testimonial, or transcript.
- The doctor is on camera and signs off compliance.
- Nothing goes live in Meta without an explicit human yes. The bootstrap never launches.
