---
name: search-term-cleanup
description: Find Google Ads search terms that spend without converting and propose negative keywords, using the Ads Insights search terms tool. Use for wasted spend, negative keyword lists, or "what are people actually searching" questions.
---

# Search term clean-up

## Steps

1. `ads_search_terms` for the last 30 days with `withoutConversions: true` and `limit: 200`.
2. `ads_search_terms` for the same range without the filter, `limit: 100`, to see what does convert and avoid excluding it.
3. If a brand or competitor was mentioned, repeat step 1 with `contains` set to it.

## Output

- Total spend on terms with no conversions, and its share of all search term spend returned.
- Terms grouped by theme (competitors, jobs and free, wrong product, wrong location, informational), each group with its spend.
- A negative keyword list ready to paste, with a suggested match type for each: exact for a single bad query, phrase for a bad word.
- Terms that converted and share words with the proposed negatives, flagged so they are not blocked by accident.

## Rules

- Terms with status `EXCLUDED` are already negatives; leave them out of the proposal.
- A term with few clicks and no conversion is not proven bad: mark anything under 10 clicks as "watch", not "exclude".
- Performance Max has no term list; if only search categories come back, say so and review the categories instead.
- Google only. Write in the person's language. This connector only reads: propose the list, never claim it was added.
