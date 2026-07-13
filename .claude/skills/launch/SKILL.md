---
name: launch
description: Build the Meta campaign from the angles, copy, and statics - one cold campaign, three ad sets (broad, interest stack, lookalike stack), the same 25-30 ads and shared 5+5 copy in each, ABO budgets, auto-features off. Builds PAUSED and never sets live without an explicit yes. Trigger with "/launch", "build the campaign in Meta", "upload the ads".
---

# launch

Turn the angles, copy, and statics into a live-ready Meta campaign following the Haynes structure. Everything is built **PAUSED**. Read `knowledge/haynes-method.md` and the client's `02-angles.md`, `03-copy.md`, and `statics/` first.

Tools: the `meta-ads` MCP (Pipeboard auth). Load tool schemas with ToolSearch `select:` before calling. If a call fails, report the exact error, do not work around it.

## Preflight

1. `get_ad_accounts` and confirm the account ID from the intake. `get_account_pages` to confirm the Facebook Page ID.
2. Confirm you have the video assets (the doctor's filmed angles) and the generated statics. If videos are not filmed yet, build the static ads now and leave video ad slots documented for a second pass.

## Structure to build (Haynes)

- **One cold campaign.** Objective `OUTCOME_LEADS` (or `OUTCOME_TRAFFIC` if the funnel is a VSL page you optimise for landing views, per the client's funnel). Status `PAUSED`.
- **ABO, not CBO.** Use ad-set-level budgets. When creating the campaign, do not enable campaign budget optimisation; set `is_adset_budget_sharing_enabled: false` if the API requires it.
- **Three ad sets**, each `PAUSED`, each with its own budget:
  1. **Broad** - no interest targeting, wide age/geo per intake.
  2. **Interest stack** - many interests, behaviours, and demographic traits loaded into one ad set (use `search_interests` / `search_behaviors` to gather them, then load them all together, do not split).
  3. **Lookalike stack** - 1% lookalikes from the clinic's best customers and qualified leads (needs source audiences in the account; if none exist yet, note it and build broad + interest first).
- Turn **off** Advantage+ creative auto-features and site links in the ad set / creative settings, except the highlight-positive-comment option.
- Set `targeting_automation: { advantage_audience: 0 }` where the API expects it.

## Creatives: the 5x5 multivariant pattern

For each ad (one per angle, aim for 25 to 30), the creative carries the shared pool: the 5 headlines and 5 body copies from `03-copy.md`, plus that angle's static or video.

Build order that avoids the DCO rejection (learned pattern):
1. **Upload media.** Statics via `upload_ad_image`. Videos via the account video endpoint, then reference the returned ad-account-scoped video ID.
2. **Create the multivariant creative** per angle with `create_ad_creative`, passing `messages` (the 5 body copies), `headlines` (the 5 headlines), and the media. This returns an `asset_feed_spec` (DCO-style) creative.
3. **Create one placeholder creative** (single message + single headline) once.
4. **Create the ads** in each ad set with the placeholder creative, `status: PAUSED`.
5. **Swap each ad** to its real multivariant creative with `update_ad` (creative_id = the multivariant one). The update bypasses the DCO check that blocks direct creation in a non-DCO ad set.

Repeat the same set of ads across all three ad sets.

## Budgets

Set ad-set budgets from the intake (in the account's minor currency unit, e.g. cents). If the intake budget is low, note in the launch plan that the read will be slower and noisier (per `knowledge/haynes-method.md`) and suggest either a wider read window or fewer ad sets.

## Before going live

1. Write `clients/<slug>/04-launch-plan.md`: campaign, ad sets, budgets, the ad-to-angle map, and the full copy pool.
2. Show the human the plan and the paused campaign in the account.
3. Only on an explicit yes, set the campaign and ad sets to `ACTIVE` (`update_campaign` / `update_adset` status ACTIVE). Never before.

## After launch (hand the loop to the operator)

Document the scaling loop from `knowledge/haynes-method.md` in the launch plan so the operator knows exactly what to do when 1 to 3 winners appear: scale to the ceiling, duplicate the ad set (keep no-reach ads, pull winners, add fresh), run the lead-quality gate, keep spares on the side.
