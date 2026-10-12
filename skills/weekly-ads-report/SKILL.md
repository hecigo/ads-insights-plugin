---
name: weekly-ads-report
description: Write a weekly advertising report for a business owner from Meta Ads, Google Ads and TikTok Ads data through the Ads Insights connector. Use when someone asks for a weekly, week-over-week or "how did ads do last week" summary.
---

# Weekly ads report

A report an owner can read in two minutes and act on. Numbers come only from Ads Insights tools; never estimate a figure the tools did not return.

## Steps

1. `ads_health`: confirm which platforms are connected. Name any that are not, and carry on with the rest.
2. `ads_insights` level `account` for the last 7 full days excluding today (`since`/`until`), with `compare: true` so the 7 days before come in the same call, with the change. Ask for `metrics: ["cpm", "conversion_rate"]`, and when Meta is connected add `"messaging_conversations", "cost_per_messaging_conversation"`. They cost no extra platform call.
3. `ads_insights` level `campaign` for the same dates with `compare: true` and the same metrics: the changes per campaign show what moved the totals. If a note says the later period may still gain conversions, say so in the report.
4. If spend fell sharply or a campaign spent nothing, `ads_delivery` for the reason.

## Report

- One line of verdict first: better, worse or flat, and why, in plain words.
- A small table per platform: spend, conversions, cost per conversion, conversion value, ROAS, each with the change against the previous week.
- For Meta, when either week has `messaging_conversations` above 0, add two columns: conversations started and cost per conversation, with their change. A shop that sells in Messenger, Instagram or WhatsApp often has 0 conversions and all its results here; then lead the Meta table with these two columns and say in the verdict that conversations are its conversion.
- The 3 campaigns that lifted results and the 3 that dragged them down, each with the number that shows it.
- At most three actions for next week, each tied to a number above.

## Rules

- ROAS is conversion value divided by spend, as a multiple (2.4x). When `conversionValue` is null the value is unknown, not zero: say so rather than showing ROAS 0.
- Do not add conversions across platforms as if they were one count: each platform attributes over its own window.
- Conversations started are not sales and not leads. Never add them to `conversions`, and never compute ROAS or a cost per sale from them. The number of orders they closed lives in the shop's own sales system, not in this connector: say so when the person asks what the conversations sold.
- Keep each platform's currency. Never add different currencies into one total.
- Write in the language the person is using.
- This connector only reads. Recommend changes; never say they were made.
