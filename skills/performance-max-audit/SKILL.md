---
name: performance-max-audit
description: Audit Google Performance Max campaigns below the campaign level: asset groups, ad strength, assets rated low, audience signals and search themes, using Ads Insights. Use when someone asks why Performance Max underperforms or what to change in it.
---

# Performance Max audit

## Steps

1. `ads_settings` level `campaign`: strategy and target of each Performance Max campaign, and its conversion goals.
2. `ads_asset_groups` for the last 30 days excluding today.
3. `ads_search_terms` for the same range, for the search categories Performance Max matched.

## Output

For each asset group, most spend first:

- Spend, conversions, conversion value, ROAS, and ad strength.
- Assets rated `LOW`, quoted, with a concrete replacement idea for each text asset; count missing asset types (fewer than 5 headlines, no video, no square image).
- Whether the audience signals and search themes match the product on the final URL; name any that look unrelated.
- Search categories that took impressions but brought nothing, as candidates for brand exclusions or account-level negatives.

End with the three changes most likely to matter, each tied to a number.

## Rules

- `LEARNING` and `PENDING` labels mean too little data, not a bad asset.
- Ad strength is Google's completeness score, not a result; weigh ROAS first.
- Google only. Write in the person's language. This skill only recommends: never claim a change was made. A budget change is a separate step: the budget-adjust skill, only in a workspace given the write scope.
