---
name: launch
description: Build the Meta campaign from the angles, copy, and statics - one cold campaign, three ad sets (broad, interest stack, lookalike stack), the same 25-30 ads and shared 5+5 copy in each, ABO budgets, auto-features off. Builds PAUSED and never sets live without an explicit yes. Trigger with "/launch", "build the campaign in Meta", "upload the ads".
---

# launch

Turn the angles, copy, and statics into a live-ready Meta campaign following the Haynes structure. Everything is built **PAUSED**. Read `knowledge/haynes-method.md` and the client's `02-angles.md`, `03-copy.md`, and `statics/` first.

Tools: the `meta-ads` MCP (the Pipeboard `meta-ads-mcp` package). Load tool schemas with ToolSearch `select:` before calling. If a call fails, report the exact error, do not work around it. This skill follows our proven NELLO creative-upload playbook exactly - do not invent a different build path.

## Auth (Pipeboard)

Daniel authorises his own Meta ad account through Pipeboard: connect the account at pipeboard.co, then set `PIPEBOARD_API_TOKEN` in the env (already referenced in `.mcp.json`). Alternatively a direct `META_ACCESS_TOKEN` works with the same package. Never check or print the token; just call the tools.

## Preflight

1. `get_ad_accounts` and confirm the account ID. `get_account_pages` to confirm the Facebook Page ID.
2. Confirm assets: the doctor's filmed video angles and the generated statics. If videos are not filmed yet, build the static ads now and document the video ad slots for a second pass.

## Structure to build (Haynes)

- **One cold campaign** (`create_campaign`), status `PAUSED`. Objective `OUTCOME_LEADS` for lead gen, or `OUTCOME_TRAFFIC` for a VSL landing-view funnel, per the client. (Video-views bin, if ever used: `OUTCOME_AWARENESS` with `THRUPLAY`.)
- **ABO, not CBO.** Ad-set-level budgets. Pass `is_adset_budget_sharing_enabled: false` on the campaign so ad-set budgets are allowed.
- **Three ad sets** (`create_adset`), each `PAUSED`, each with its own budget in the account's **minor currency unit** (cents; SGD 50/day = 5000):
  1. **Broad** - no interest targeting, wide age/geo.
  2. **Interest stack** - many interests, behaviours, demographic traits in ONE ad set (`search_interests` / `search_behaviors` to gather, then load together, do not split).
  3. **Lookalike stack** - 1% lookalikes from best customers + qualified leads (needs source audiences; if none, note it and ship broad + interest first).
- On every ad set: `optimization_goal: LEAD_GENERATION` (leads) with `billing_event: IMPRESSIONS`; `targeting_automation: { advantage_audience: 0 }`.
- Turn **off** Advantage+ creative auto-features and site links, except the highlight-positive-comment option.

## Creatives: the 5x5x5 multivariant + placeholder-swap (our exact playbook)

Every creative carries a shared pool of **5 primary texts + 5 headlines + 5 descriptions** (Kennedy angles: pain / desire / curiosity / social proof / urgency), the same pool across all 25-30 ads. Never single-variant. This is the NELLO creative-upload playbook, followed exactly.

1. **Upload media.** Statics: `upload_ad_image` → use the returned `image_hash`. Videos: upload to the account `advideos` endpoint → use the returned ad-account-scoped `video_id` (page-uploaded IDs do not work; fetch a fresh thumbnail immediately, Meta CDN thumbnails expire fast).
2. **Create the multivariant creative** per angle: `create_ad_creative(account_id, page_id, video_id | image_hash, link_url, call_to_action_type: "LEARN_MORE", messages: [5 primary texts], headlines: [5 headlines], descriptions: [5 descriptions])`. Returns a creative with `asset_feed_spec` (Meta classifies this as DCO).
3. **Create one placeholder creative** once: `create_ad_creative(... message: "Placeholder", headline: "Placeholder")` (single-variant `object_story_spec`).
4. **Create the ads** with the placeholder: `create_ad(account_id, name, adset_id, creative_id: <placeholder>, status: "PAUSED")`. Direct creation with the multivariant creative in a non-DCO ad set fails with **error 1885998** - that is why we use the placeholder first.
5. **Swap each ad** to its real multivariant creative: `update_ad(ad_id, creative_id: <multivariant>)`. `update_ad` bypasses the DCO check. Each ad now shows "Primary text (1 of 5)" in Ads Manager.

Repeat the same set of ads across all three ad sets.

## Budgets

Set ad-set budgets from the intake (in the account's minor currency unit, e.g. cents). If the intake budget is low, note in the launch plan that the read will be slower and noisier (per `knowledge/haynes-method.md`) and suggest either a wider read window or fewer ad sets.

## Before going live

1. Write `clients/<slug>/04-launch-plan.md`: campaign, ad sets, budgets, the ad-to-angle map, and the full copy pool.
2. Show the human the plan and the paused campaign in the account.
3. Only on an explicit yes, set the campaign and ad sets to `ACTIVE` (`update_campaign` / `update_adset` status ACTIVE). Never before.

## After launch (hand the loop to the operator)

Document the scaling loop from `knowledge/haynes-method.md` in the launch plan so the operator knows exactly what to do when 1 to 3 winners appear: scale to the ceiling, duplicate the ad set (keep no-reach ads, pull winners, add fresh), run the lead-quality gate, keep spares on the side.
