# hecigo Ads Insights for Claude

Skills and a read-only connector for Meta Ads, Google Ads and TikTok Ads, from [hecigo](https://hecigo.com). Version 0.2.6.

The connector is hecigo's hosted MCP server at `https://ads.hecigo.com/mcp`: sign in with Google when asked, then connect your ad accounts. It only reads; it cannot change campaigns, budgets or ads.

## Skills

- `meta-vn-diagnosis`: Diagnose why Meta Ads cost per result went up and decide whether to scale, hold, fix or stop each campaign or ad set, for sellers in Vietnam, including shops that sell in the Messenger inbox.
- `performance-max-audit`: Audit Google Performance Max campaigns below the campaign level: asset groups, ad strength, assets rated low, audience signals and search themes, using Ads Insights.
- `roas-target-audit`: Compare each campaign's configured target ROAS or target CPA with its actual results, using Ads Insights settings and performance.
- `search-term-cleanup`: Find Google Ads search terms that spend without converting and propose negative keywords, using the Ads Insights search terms tool.
- `weekly-ads-report`: Write a weekly advertising report for a business owner from Meta Ads, Google Ads and TikTok Ads data through the Ads Insights connector.

## Install

**Claude on the web, Desktop, mobile and Cowork:** open **Customize → Plugins**, choose **Add → Add marketplace → Add from a repository**, enter `hecigo/ads-insights-plugin` and choose **Sync**, then **Add** hecigo Ads Insights. If the connector is not connected yet, connect it from the plugin's **Connectors** tab. Skills need **Cloud code execution and file creation** turned on under **Settings → Capabilities**.

**Claude Code:**

```
/plugin marketplace add hecigo/ads-insights-plugin
/plugin install hecigo-ads-insights@hecigo
```

Step by step, in Vietnamese and English: [the guide](https://ads.hecigo.com/guide#bo-skill). ChatGPT, Gemini, Cursor and VS Code do not load Claude skills; add `https://ads.hecigo.com/mcp` as a connector there instead.

## Data and privacy

The skills are written instructions; they run nothing on your machine and send nothing anywhere themselves. The plugin declares one connector, hecigo's MCP server at `https://ads.hecigo.com/mcp`. When a skill asks it for numbers, that server reads the Meta Marketing API, Google Ads API, TikTok Business API, Google Analytics Data API or Search Console API with the access you granted on each platform's own consent screen, and returns the figures to Claude. Every tool only reads. hecigo keeps your sign-in email and sealed access tokens, not your reporting numbers, which are fetched when you ask. Details, retention and deletion: [hecigo's privacy policy](https://hecigo.com/privacy/).

## About this repository

It is generated from hecigo's own repository on every release, so changes made here directly are overwritten. Questions and problems: [hi@hecigo.com](mailto:hi@hecigo.com).

MIT licensed.
