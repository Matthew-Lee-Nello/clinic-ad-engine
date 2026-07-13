---
name: market-research
description: Best-in-class research agent for a clinic treatment. Produces a buyer-spectrum market read (awareness + sophistication) and scrapes the Meta Ads Library for what competitors are running and for how long. Trigger with "/market-research", "research this treatment", "what's running in the ad library for X".
---

# market-research

Two jobs: read the market on the buyer spectrum, and scrape the Meta Ads Library for structural inspiration. Output to `clients/<slug>/01-research.md`.

## Part 1: buyer-spectrum market read

Using web research (Exa or Tavily) plus the intake, work out for THIS treatment in THIS country:

- **Awareness stage.** Does the public know the treatment exists, know the mechanism, or are they comparing providers? This sets whether a simple claim or a unique-mechanism angle converts (see `knowledge/haynes-method.md`, buyer spectrum).
- **Sophistication stage.** How many providers are already making similar claims? The more crowded, the more you must lead with a specific mechanism and process.
- **The real questions the market asks** about this treatment (pain, cost, recovery, safety, "does it work for me"). Pull these from forums, search suggestions, and competitor pages.
- **The doctor's leverage.** Where the doctor's real point of difference (from the intake) meets a gap the market cares about.

Do not invent numbers. Cite where a claim comes from.

## Part 2: Meta Ads Library scrape

Goal: see what is already running in and around this niche, and how long ads have been live (longevity is a rough signal a competitor keeps paying for an ad). Structure and format inspiration only. Never lift a competitor's angle wholesale, and never copy anything non-compliant.

Preferred tool: **Apify** Facebook Ads Library scraper.

1. Find the actor: `search-actors` for "facebook ads library". Common actor: `apify/facebook-ads-scraper` or an equivalent Ad Library actor.
2. `fetch-actor-details` to get the input schema.
3. `call-actor` with input for the country and search terms (treatment names, competitor page names from the intake). Set the ad-active status and country.
4. `get-dataset-items` to pull results. Capture for each ad: page name, ad copy, media type (image/video), first-seen date (for longevity), and the creative angle.

Fallback for a single known Ad Library URL: **Crawl4AI** `md` on the URL, or `crawl` for a set of URLs.

Fallback if scraping is blocked: use the Meta Ad Library website directly and record what you can, and note the limitation. Never fabricate ads that are not there.

## Output (`01-research.md`)

- Buyer-spectrum verdict: awareness stage, sophistication stage, and the messaging implication.
- The top real questions the market asks.
- A short table of competitor ads found: page, media type, longevity, the angle they use, and whether it would be compliant here.
- Three to five structural or format observations worth borrowing (not angles to copy).
- Where the doctor's point of difference gives an opening.

Note honestly if the exact-niche library is thin or empty. That is common and expected in restricted niches: it means you generate angles from first principles (buyer spectrum + point of difference), not from a swipe file.
