---
name: meta-vn-diagnosis
description: Diagnose why Meta Ads cost per result went up and decide whether to scale, hold, fix or stop each campaign or ad set, for sellers in Vietnam, including shops that sell in the Messenger inbox. Splits the cost change into CPM, link CTR and conversion rate, checks frequency and creative fatigue, and states its thresholds. Use when someone asks why CPA, cost per message or cost per order rose, whether to scale or turn off ads, or says "vì sao giá tin nhắn tăng", "CPA tăng", "nên scale hay tắt", "quảng cáo bị mỏi chưa".
---

# Meta diagnosis for sellers in Vietnam

The answer an owner wants: why it got more expensive, which part is to blame, and what to do with each campaign. Numbers come only from Ads Insights tools; never estimate a figure the tools did not return.

## Steps

1. `ads_health`: confirm Meta is connected. If not, pass on the connect link and stop.
2. `ads_settings` provider `meta`, level `adset`. For each ad set note `optimizationGoal`, `bidding`, `budget`, `audiences` and any note that the budget comes from the campaign (Advantage campaign budget).
3. Decide what one result is, per ad set. Ask `metrics: ["results", "cost_per_result"]` in step 4: that is Ads Manager's own Results column, and each row's `resultType` names what Meta counted, in Meta's own words (seen on a real account: `actions:post_engagement`, `page_visit_view`). Use it rather than guessing:
   - a shop that sells in the inbox: the result is conversations started; also ask `new_messaging_contacts` to see the cost of a new customer;
   - `results` is null for an ad set with spend: Meta counted nothing as a result there, or ad sets with different goals were added together. Read at level `adset` to tell them apart, and never treat null as zero;
   - reach, engagement, page likes or video views: say this skill judges sales and messages, and judge those ad sets only by their own goal's cost.
   If the person's own idea of a result differs from Meta's (they count orders, Meta counts messages), say so and use theirs for decisions.
4. `ads_insights` provider `meta`, level `adset` (or `campaign` where the budget sits on the campaign), for the last 7 full days excluding today (`since`/`until`) with `compare: true`, which reads the 7 days before in the same call and gives each row's earlier value, later value and change under `comparison`. Each period is its own report, so reach and frequency are exact for both. Ask:
   - `metrics: ["results", "cost_per_result", "cpm", "reach", "frequency", "messaging_conversations", "new_messaging_contacts"]`
   - `metaFields: ["inline_link_clicks", "inline_link_click_ctr"]`
   - for inbox shops, `actionTypes: ["onsite_conversion.messaging_user_depth_2_message_send", "onsite_conversion.messaging_user_depth_3_message_send"]`: conversations where the person sent a second and a third message.
5. `ads_insights` level `ad` for the last 14 full days with `byDay: true` and the same `metaFields` plus `quality_ranking`, `engagement_rate_ranking`, `conversion_rate_ranking`, and `metrics: ["frequency", "reach", "cpm"]` for the same 14 days without `byDay`. This is the fatigue check.
6. If spend fell or an ad set spent nothing, `ads_delivery` before anything else.

## Split the cost change

Use link clicks, never `clicks` or `ctr`: on Meta those count every click, image taps and "see more" included. On one real account an ad showed 7.19% CTR against 0.04% link CTR.

For each period:

- CPM = spend / impressions × 1000
- link CTR = inline_link_clicks / impressions
- CVR = results / inline_link_clicks, with results from Meta's `results` column
- cost per result = CPM / 1000 / (link CTR × CVR). This is an identity: the three parts always multiply back to the cost.

Compare the two periods with logarithms so the parts add up exactly:

- total = ln(cost₂ / cost₁)
- CPM part = ln(CPM₂ / CPM₁)
- CTR part = −ln(CTR₂ / CTR₁)
- CVR part = −ln(CVR₂ / CVR₁)

Report each part as its share of the total change, and name the largest. A part with the opposite sign worked against the change, and the others then add to more than 100%: say it that way (cost fell 12%: CPM 90%, CVR 25%, link CTR −15%). When an ad set has no link clicks, or fewer link clicks than results (people can message a Page without a counted link click), do not split CTR from CVR: use results per 1,000 impressions as one part beside CPM, and say why.

What each part points to:

- **CPM**: the auction got dearer or the audience is used up. Seasonal pressure in Vietnam is real: Tết, and the sale days 9/9, 10/10, 11/11, 12/12 and payday mid and end of month. Compare against the same days last month or last year before calling it a problem. A narrow audience with frequency climbing also raises CPM.
- **link CTR**: the ad stopped stopping people. Check the fatigue signs below.
- **CVR**: the problem is after the click, and changing ads will not fix it. Website: price, stock, page speed, a broken pixel. Inbox: slow replies, nobody answering at night, a welcome message that asks too much. Say so plainly.

## Fatigue

An ad is fatigued when all three hold over the last 14 days:

- frequency is 3 or more for a cold audience, or 6 or more when the ad set includes custom audiences (retargeting);
- link CTR over the last 7 days is at least 20% below its first 7 days;
- CPM did not fall in the same time, so the drop is not cheaper, worse inventory.

Frequency high but link CTR steady: not fatigued yet, watch it. Rankings that say `BELOW_AVERAGE_…` support the call. `UNKNOWN` means Meta has not shown the ad enough to rank it: say so and do not read it as bad.

## Scale, hold, fix or stop

The reference cost, in this order: the cost per result the person names (their break-even or target); the ad set's own cost cap or target from `bidding`; else the account's cost per result over the 30 days before the last 7, for the same result. Say which one you used.

Judge where the budget sits: the ad set, or the campaign when it uses Advantage campaign budget.

- **Not enough data → hold.** Fewer than 10 results in the last 7 days and spend under 3 × the reference. Say how much more data a call needs.
- **Scale.** Cost per result at most 80% of the reference, at least 10 results in 7 days, 7-day frequency under 2.5, and the last 3 days not worse than the reference. Suggest raising the budget about 20%, then waiting 3 days before the next step. Larger jumps can send an ad set back into Meta's learning phase; this connector cannot read learning status, so point to Ads Manager for it.
- **Hold.** Between 80% and 120% of the reference, or it would scale but frequency or volume says not yet.
- **Fix.** Between 120% and 150% of the reference; or the CVR part drives the rise (fix after the click); or an ad is fatigued (new creative, keep the ad set).
- **Stop.** At least 150% of the reference with spend of 3 × the reference or more in 7 days and no improvement in the last 3 days; or spend of 3 × the reference with no result at all.

These thresholds are this skill's defaults, not Meta rules. If the person gives their own, use theirs.

## Inbox shops

- A conversation started is not an order. The orders closed in the inbox live in the shop's own records (page inbox labels, a sales sheet, the POS), not in this connector. Ask for the number of orders in the same 7 days to get a real cost per order; never assume a close rate.
- Depth 2 and depth 3 conversations show how many people actually talked. A cost per conversation that looks cheap with almost no depth-2 replies is a worse result than it seems.
- `new_messaging_contacts` is people messaging for the first time; `messaging_conversations` counts conversations. Do not add them, and never add messaging counts to `conversions`.

## Output

- One line first: why the cost moved, in plain words, and the part that drove it with its share.
- A table per period pair: spend, results, cost per result, CPM, link CTR, CVR, frequency, with the change.
- Fatigued ads, each with frequency, link CTR first week against last week, and CPM.
- A table of decisions: campaign or ad set, scale / hold / fix / stop, the numbers behind it, the next step.
- What is missing for a firmer call: more days, the shop's order count, a target cost.

## Rules

- Meta only. For Google or TikTok use their own reports; never add results across platforms.
- Keep the account currency. VND has no decimals: write 1.527 ₫ in Vietnamese and ₫1,527 in English.
- Write in the language the person is using.
- This skill only recommends. Never say a change was made. A budget change is a separate step: the budget-adjust skill, only in a workspace given the write scope.
