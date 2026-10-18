---
name: roas-target-audit
description: Compare each campaign's configured target ROAS or target CPA with its actual results, using Ads Insights settings and performance. Use when someone asks whether campaigns hit their targets, what a campaign's target really is, or which bidding targets to revisit.
---

# ROAS and CPA against target

The target lives in the platform's bidding settings, not in the campaign name. A name like `ROAS_22` is a label someone typed once.

## Steps

1. `ads_settings` (Google defaults to level `campaign`; Meta and TikTok default to `adset`, where their bidding lives). Note for each row: `bidding.strategy`, `bidding.targetRoas`, `bidding.targetCpa`, `bidding.portfolio`, `conversionGoals`.
2. `ads_insights` at the same level for the last 30 days excluding today: spend, conversions, cost per conversion, conversion value, ROAS.
3. Match rows by id, not by name.

## Output

A table: campaign, strategy, target, actual, gap in percent, spend. Then:

- Campaigns more than 20% worse than target, most spend first, with a likely reason from the settings (too few conversions to learn, a target set far from reality, the wrong conversion goal, a shared portfolio target).
- Campaigns beating target by a wide margin, where the target may be holding back volume.
- Campaigns with no target at all, and what they optimise for instead.

## Rules

- `targetRoas` is a multiple: 0.23 means 23%, 2.2 means 220%. Show both forms.
- A portfolio strategy's target applies to every campaign in it; say which campaigns share it.
- Under 30 conversions in the window, call the comparison unreliable rather than drawing a conclusion.
- Write in the person's language. This skill only recommends; suggest target changes, never claim to make them. A budget change is a separate step: the budget-adjust skill, only in a workspace given the write scope.
