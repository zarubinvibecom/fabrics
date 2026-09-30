# Idea collection & monitoring stage (content factory for a vibe-coding blog) — status as of 2026-09-30

Method note: GitHub star counts and archive status below were pulled live from the GitHub search API on 2026-09-30 (source for each = the repo URL). Licenses marked "(lic. unverified)" are from prior knowledge and were NOT re-checked in this session. n8n.io, docs.x.com and several blogs were blocked by the egress proxy, so some claims rely on search-result snippets (flagged).

## 1. Which GitHub repos / tools exist for monitoring & collection?

### Takeaway
A solo creator can cover ~80% of sources with a free self-hosted stack: RSSHub (turn anything into RSS) + Miniflux/FreshRSS (store/filter) + yt-dlp/youtube-transcript-api (YouTube) + HN Firebase API + GitHub-Trending RSS + n8n (glue) + an LLM for scoring. The strongest "all-in-one" ready-mades in 2026 are `mvanhorn/last30days-skill` (Claude Code skill, 63k stars) and `sansan0/TrendRadar` (62k stars). X/Twitter, Reddit and YouTube-from-cloud are the three sources that now need paid APIs, proxies, or scraping services.

### Cited Findings

**Feed backbone (RSS layer)**
- RSSHub — https://github.com/DIYgod/RSSHub — 46.4k stars, TypeScript, active (pushed 2026-09-30). "Everything is RSSible": routes for YouTube, Telegram channels, Twitter, TikTok, Instagram, etc. AGPL-3.0 (lic. unverified). Pros: one self-hosted Docker service turns most sources into RSS; cons: social routes (X, Instagram) need your own cookies/tokens and break often. — [GitHub](https://github.com/DIYgod/RSSHub)
- Miniflux — https://github.com/miniflux/v2 — 9.8k stars, Go + PostgreSQL, "minimalist and opinionated feed reader". Apache-2.0 (lic. unverified). Pros: tiny, REST API, webhooks, filter rules — good as the "inbox" feeding n8n/LLM. — [GitHub](https://github.com/miniflux/v2)
- FreshRSS — https://github.com/FreshRSS/FreshRSS — 16.2k stars, PHP, self-hostable aggregator with WebSub. AGPL-3.0 (lic. unverified). — [GitHub](https://github.com/FreshRSS/FreshRSS)
- tt-rss — https://github.com/tt-rss/tt-rss — 852 stars (new repo home created Oct 2025 after moving off the old self-hosted Gitea). — [GitHub](https://github.com/tt-rss/tt-rss)
- Folo (ex-Follow) — https://github.com/RSSNext/Folo — 39.0k stars, "the AI RSS Reader" from the RSSHub team; AI summaries/translation over feeds. — [GitHub](https://github.com/RSSNext/Folo)
- Glance — https://github.com/glanceapp/glance — 37.3k stars, Go, self-hosted dashboard with built-in widgets for RSS, Reddit, YouTube, HN. Good as a human-readable "radar screen". — [GitHub](https://github.com/glanceapp/glance)
- changedetection.io — https://github.com/dgtlmoon/changedetection.io — 34.7k stars, Python, self-hosted page-change monitor with RSS output and notifications; free self-host or paid SaaS. Use-case: watch competitor pricing pages, changelogs (Cursor/Lovable/Bolt/Replit changelog pages without RSS), docs. — [GitHub](https://github.com/dgtlmoon/changedetection.io)
- Huginn — https://github.com/huginn/huginn — 50.0k stars, Ruby, "agents that monitor and act on your behalf" (older IFTTT-style self-host). MIT (lic. unverified). Largely superseded by n8n for new setups (inference). — [GitHub](https://github.com/huginn/huginn)
- GitHub Trending RSS — https://mshibanami.github.io/GitHubTrendingRSS/ — unofficial feeds per language/period regenerated daily by GitHub Actions. — [GitHub](https://github.com/mshibanami/GitHubTrendingRSS)

**Orchestration**
- n8n — https://github.com/n8n-io/n8n — 206k stars, "fair-code" (Sustainable Use License, not OSI open source), self-host free, 400+ integrations, native AI/MCP nodes. — [GitHub](https://github.com/n8n-io/n8n)
- Zie619/n8n-workflows — 56.9k stars, dump of "all of the workflows of n8n I could find". — [GitHub](https://github.com/Zie619/n8n-workflows)
- enescingoz/awesome-n8n-templates — 25.7k stars, 280+ free templates. — [GitHub](https://github.com/enescingoz/awesome-n8n-templates)

**YouTube**
- yt-dlp — https://github.com/yt-dlp/yt-dlp — 194.5k stars; can list channel uploads (`--flat-playlist`), dump metadata JSON (views, duration, upload date) and auto-subtitles without an API key. Unlicense (lic. unverified). — [GitHub](https://github.com/yt-dlp/yt-dlp)
- youtube-transcript-api — https://github.com/jdepoix/youtube-transcript-api — 8.4k stars, Python, no API key or headless browser. MIT (lic. unverified). — [GitHub](https://github.com/jdepoix/youtube-transcript-api)
  - RISK: YouTube blocks most cloud-provider IPs (AWS/GCP/Azure) → `RequestBlocked`/`IpBlocked`; library recommends rotating *residential* proxies (Webshare "Residential", not "Proxy Server"/"Static Residential"); a retry-on-block was added. Users still report blocks even with Webshare. — [PyPI](https://pypi.org/project/youtube-transcript-api/); [Issue #511](https://github.com/jdepoix/youtube-transcript-api/issues/511); [Issue #504](https://github.com/jdepoix/youtube-transcript-api/issues/504)
- scrapetube — https://github.com/dermasmid/scrapetube — 524 stars, scrape channels/playlists/search without API. — [GitHub](https://github.com/dermasmid/scrapetube)
- Native YouTube channel RSS (`https://www.youtube.com/feeds/videos.xml?channel_id=...`) — free new-video detection (prior knowledge; no source fetched this session).

**Reddit**
- PRAW — https://github.com/praw-dev/praw — 4.3k stars, Python Reddit API Wrapper (needs OAuth app). — [GitHub](https://github.com/praw-dev/praw)
- Access status: see section 4 — OAuth gated since Nov 2025; `.json` returns 403 in 2026; `.rss` still answers but rate-limited (429) since June 2026.

**Hacker News**
- Official HN API (Firebase) — https://github.com/HackerNews/API — 13.3k stars, free, no key. (Algolia HN Search API `hn.algolia.com/api` is the usual choice for keyword search — prior knowledge.) — [GitHub](https://github.com/HackerNews/API)

**X/Twitter scrapers** (see section 4 for cost & risk)
- twikit — https://github.com/d60/twikit — 4.7k stars, uses internal API, no key, needs account login. — [GitHub](https://github.com/d60/twikit)
- twscrape — https://github.com/vladkens/twscrape — 2.8k stars, multi-account rotation, rate-limit handling. — [GitHub](https://github.com/vladkens/twscrape)
- twitter-api-client — https://github.com/trevorhobenshield/twitter-api-client — 1.9k stars. — [GitHub](https://github.com/trevorhobenshield/twitter-api-client)
- Nitter — https://github.com/zedeus/nitter — 14.5k stars, **ARCHIVED** (read-only) per GitHub API on 2026-09-30 → do not build on Nitter RSS. — [GitHub](https://github.com/zedeus/nitter)
- snscrape — https://github.com/JustAnotherArchivist/snscrape — 5.5k stars; Twitter module broken since 2023 (prior knowledge, flag). — [GitHub](https://github.com/JustAnotherArchivist/snscrape)

**TikTok / Instagram**
- instaloader — https://github.com/instaloader/instaloader — 13.5k stars, Instagram posts+metadata. — [GitHub](https://github.com/instaloader/instaloader)
- TikTokDownloader — https://github.com/JoeanAmier/TikTokDownloader — 16.4k stars, TikTok/Douyin data collection. — [GitHub](https://github.com/JoeanAmier/TikTokDownloader)
- MediaCrawler — https://github.com/NanmiCoder/MediaCrawler — 66k stars, Chinese platforms (Xiaohongshu, Douyin, Bilibili...) — irrelevant for EN/RU vibe-coding unless tracking Chinese AI-coding trends. — [GitHub](https://github.com/NanmiCoder/MediaCrawler)
- ScrapeCreators (paid API, used by last30days for TikTok/IG/Threads/LinkedIn): 10,000 free calls/month then pay-as-you-go. — [last30days README](https://github.com/mvanhorn/last30days-skill)

**Google Trends**
- pytrends — https://github.com/GeneralMills/pytrends — 3.7k stars, **ARCHIVED** as of 2026-09-30 → unmaintained. — [GitHub](https://github.com/GeneralMills/pytrends)

**Product Hunt**
- Product Hunt API v2 (GraphQL, `api.producthunt.com/v2/api/graphql`): free developer token, but "by default must not be used for commercial purposes" — email hello@producthunt.com for business use. Apify actors exist as wrappers (e.g., `mattdef/producthunt-scraper` RSS+GraphQL). — [PH API docs](https://api.producthunt.com/v2/docs); [Apify](https://apify.com/mattdef/producthunt-scraper)

**Web scraping / extraction for LLMs**
- Firecrawl — https://github.com/firecrawl/firecrawl — 187k stars; AGPL-3.0 self-host or paid cloud (lic. unverified). — [GitHub](https://github.com/firecrawl/firecrawl)
- Crawl4AI — https://github.com/unclecode/crawl4ai — 84.6k stars, open-source, site → LLM-ready Markdown. — [GitHub](https://github.com/unclecode/crawl4ai)
- Crawlee — https://github.com/apify/crawlee — 25.9k stars, Node.js crawler lib (Apify). — [GitHub](https://github.com/apify/crawlee)
- Jina Reader — https://github.com/jina-ai/reader — 12.1k stars, prefix `https://r.jina.ai/` for LLM-friendly page text. — [GitHub](https://github.com/jina-ai/reader)
- trafilatura — https://github.com/adbar/trafilatura — 6.9k stars, article text extraction from RSS/pages. — [GitHub](https://github.com/adbar/trafilatura)
- SearXNG — https://github.com/searxng/searxng — 37.8k stars, self-hosted metasearch (free alternative to paid search APIs). — [GitHub](https://github.com/searxng/searxng)

**AI research / digest agents (the "summarize + synthesize" layer)**
- last30days-skill — https://github.com/mvanhorn/last30days-skill — 63.3k stars (created Jan 2026), MIT. Claude Code / agent skill: researches a topic across Reddit (real upvotes + top comments), HN, Polymarket, GitHub, arXiv, Techmeme, Digg (free, no key) plus X (official API credits, browser cookies or third-party keys), YouTube (via yt-dlp), TikTok/IG/Threads/Pinterest/LinkedIn (ScrapeCreators), Bluesky, Perplexity, Brave Search (2,000 free queries/month). Install: `/plugin marketplace add mvanhorn/last30days-skill`. — [GitHub README](https://github.com/mvanhorn/last30days-skill)
- TrendRadar — https://github.com/sansan0/TrendRadar — 62.6k stars, Python, Docker; "AI-driven public opinion & trend monitor": aggregates multi-platform hot lists + RSS, keyword filtering, AI filtering/translation/briefs, MCP server, push to Telegram/email/Slack/ntfy etc. Mostly Chinese-platform hot lists by default; RSS + keywords make it adaptable. — [GitHub](https://github.com/sansan0/TrendRadar)
- AIHOT — https://github.com/KKKKhazix/AIHOT — 4.0k stars (created 2026-09-28, very new), TypeScript: "a website framework that finds hot topics and writes a daily report itself — swap in your sources and curation criteria". — [GitHub](https://github.com/KKKKhazix/AIHOT)
- daily.dev — https://github.com/dailydotdev/daily — 20.1k stars, dev news feed aggregator (tagged `ai-news`, `vibe-coding-friendly`) — useful as a source, not self-host. — [GitHub](https://github.com/dailydotdev/daily)
- Kagi Kite — https://github.com/kagisearch/kite-public — 1.1k stars, open news app with clustered daily stories. — [GitHub](https://github.com/kagisearch/kite-public)
- GPT Researcher — https://github.com/assafelovic/gpt-researcher — 29.8k stars, autonomous deep research with any LLM, MCP server. — [GitHub](https://github.com/assafelovic/gpt-researcher)
- dzhng/deep-research — 19.7k stars, minimal deep-research agent. — [GitHub](https://github.com/dzhng/deep-research)
- DeerFlow — https://github.com/bytedance/deer-flow — 83.3k stars, long-horizon research "SuperAgent". — [GitHub](https://github.com/bytedance/deer-flow)
- Exa MCP server — https://github.com/exa-labs/exa-mcp-server — 5.1k stars; Tavily MCP — https://github.com/tavily-ai/tavily-mcp — 2.4k stars (search APIs, paid with free tiers). — [Exa](https://github.com/exa-labs/exa-mcp-server); [Tavily](https://github.com/tavily-ai/tavily-mcp)
- Open Notebook — https://github.com/lfnovo/open-notebook — 39.7k stars, open-source NotebookLM alternative (drop transcripts/articles, chat, generate). — [GitHub](https://github.com/lfnovo/open-notebook)
- Karakeep — https://github.com/karakeep-app/karakeep — 29.4k stars, self-hosted bookmark-everything with AI auto-tagging — good "manual capture" inbox for ideas you stumble on. — [GitHub](https://github.com/karakeep-app/karakeep)

**Apify actors (paid, pay-per-result)**
- apidojo Tweet Scraper V2 — https://apify.com/apidojo/tweet-scraper — $0.40 per 1,000 tweets, 30–80 tweets/sec, min 50 tweets per query; free Apify users limited to 5 runs/month × 10 items (snippet-level; page not fetched). — [Apify](https://apify.com/apidojo/tweet-scraper); [use-apify.com comparison](https://use-apify.com/docs/best-apify-actors/best-twitter-scrapers)

### Inferences
- Recommended cheap stack for one person (~$0–30/month): VPS ($5) running Docker: RSSHub + Miniflux + changedetection.io + n8n + Postgres; YouTube via channel RSS + yt-dlp (run transcripts from a home machine or with residential proxy); HN/GitHub/PH via free APIs/RSS; X via Apify ($0.40/1k) for a curated list of ~50 accounts; weekly deep dive with last30days in Claude Code.
- Avoid building on archived projects (Nitter, pytrends) and on snscrape for X.

### Gaps
- Licenses were not re-verified live; stars for some candidates (e.g., ourongxing/newsnow, Telegram-specific monitors like Telethon-based tools) not retrieved.
- Could not fetch n8n.io template pages (egress blocked) to get view/usage counts.

## 2. How do people build "trend radar" / "idea engine" systems (n8n, Reddit communities, Claude Code)?

### Takeaway
The dominant pattern (visible in n8n's official template library and Gumroad bundles) is: Schedule trigger → pull RSS/Reddit/YouTube/X/Perplexity → dedupe → LLM extracts insights + scores virality/fit → write to Google Sheets/Airtable → daily email/Slack/Telegram digest. Claude Code users increasingly replace n8n with skills (last30days) + cron/Trigger.dev. Direct Reddit thread quotes could not be fetched this session.

### Cited Findings
- n8n template #2903 "YouTube outlier detector": monitors competitor channels and flags videos that significantly outperform the channel's average views. — [n8n.io](https://n8n.io/workflows/2903-youtube-outlier-detector-find-trending-content-based-on-your-competitors/) (snippet only)
- n8n template #15253 "Score daily viral YouTube Shorts ideas using Reddit, RSS, and DeepSeek AI": harvests trending topics from multiple RSS news feeds + Reddit hot posts, AI scores each trend against the channel's historical performance patterns, picks the best daily ideas. — [n8n.io](https://n8n.io/workflows/15253-score-daily-viral-youtube-shorts-ideas-using-reddit-rss-and-deepseek-ai/) (snippet only)
- n8n template #12703 "Daily AI & automation content digest from YouTube, Reddit, X and Perplexity with OpenAI and Airtable": aggregates trending content, OpenAI extracts insights, archives in Airtable, sends HTML email. — very close to what a vibe-coding blog needs. — [n8n.io](https://n8n.io/workflows/12703-create-a-daily-ai-and-automation-content-digest-from-youtube-reddit-x-and-perplexity-with-openai-and-airtable/)
- n8n #7923: pulls AskReddit posts, dedupes, computes a custom virality score, writes candidates to Google Sheets. — [n8n.io](https://n8n.io/workflows/7923-create-viral-youtube-content-from-reddit-posts-with-gpt-4o-and-google-sheets/)
- Other templates: #5375 content-strategy reports from Reddit/YouTube/X with Gemini; #4373 Reddit trend analysis with GPT-4 → Slack/Gmail; #3609 summarize YouTube videos into structured content ideas → Airtable; #10808 YouTube content strategy with Apify + Sheets; #8140 Reddit scraping + AI analysis + Sheets; #10007 curate from Reddit & RSS with GPT-4.1-mini. — [n8n.io #5375](https://n8n.io/workflows/5375-generate-content-strategy-reports-analyzing-reddit-youtube-and-x-with-gemini/); [#4373](https://n8n.io/workflows/4373-automate-reddit-trend-analysis-with-gpt-4-and-slackgmail-distribution/); [#3609](https://n8n.io/workflows/3609-summarize-youtube-videos-into-structured-content-ideas-with-ai-and-airtable/); [#10808](https://n8n.io/workflows/10808-automate-youtube-content-strategy-with-ai-apify-and-google-sheets/); [#8140](https://n8n.io/workflows/8140-automate-content-research-with-reddit-scraping-ai-analysis-and-google-sheets/); [#10007](https://n8n.io/workflows/10007-curate-learning-content-from-reddit-and-rss-with-gpt-41-mini-and-google-sheets/)
- Commercial "Reddit Content Hub" workflow scrapes r/n8n, r/AI_Agents, r/ArtificialIntelligence, r/mcp and classifies posts into a hub (Gumroad) — evidence of a market for these setups. — [Gumroad](https://semah.gumroad.com/l/Reddit-content-hub)
- Claude-API Reddit monitor pattern: Python on a schedule, Claude scores every post for relevance + sentiment, alerts only above threshold. — [DEV Community](https://dev.to/henryknight_dev/how-i-automated-reddit-monitoring-with-the-claude-api-full-code-1g7g)
- AI news digest agent with Claude Code + Trigger.dev: checks a YouTube channel for new uploads every 8 hours, Claude summarizes, emails a digest. — [MindStudio blog](https://www.mindstudio.ai/blog/ai-news-digest-agent-claude-code-trigger-dev)
- YouTube transcript MCP server with a Claude Code sub-agent guide ("YouTube Transcript Analyzer"). — [Glama](https://glama.ai/mcp/servers/@hancengiz/youtube-transcript-mcp/blob/6f4e95a47e1510a8d5ff840f64b95b7b5a2b9898/CLAUDE_CODE_AGENT_GUIDE.md)
- Content-gap analyzer as a Claude Code subagent. — [GenAI Unplugged](https://genaiunplugged.substack.com/p/content-gap-analyzer-ai-agent-claude-code)

### Inferences
- A good vibe-coding pipeline = template #12703 architecture + outlier logic from #2903 + scoring prompt from #15253, with Postgres/Airtable as backlog.
- Claude Code users can skip n8n: a `/loop`-style scheduled Claude Code session or cron running last30days for "vibe coding", "Claude Code", "Cursor" weekly, writing into an Obsidian/markdown backlog.

### Gaps
- Could not retrieve direct quotes from r/n8n, r/automation, r/ContentCreators, r/SideProject, r/ClaudeAI, r/vibecoding threads (reddit.com not surfaced by search, and Reddit JSON is 403). Report writer should not cite specific Reddit quotes from these notes.

## 3. How to score/prioritize and store ideas?

### Takeaway
The industry-standard virality signal is the **outlier score = video views / channel's average (or median) views**, popularized by 1of10 (surfaces 10x–100x outliers), vidIQ and ViewStats. For text sources, use velocity (upvotes/points per hour since posting), cross-source mentions (same topic on HN + Reddit + X = cluster strength), and LLM-judged niche fit. Storage: Google Sheets/Airtable in most n8n templates; Postgres (Miniflux already uses it) or Obsidian/markdown for Claude Code setups.

### Cited Findings
- 1of10: built on "62 billion analysed YouTube views", scores each video against its own channel average, surfaces those 10x–100x above. Pricing: Free (outlier search + 3 tracked channels), Basic $29/mo ($349/yr), Pro $69/mo ($828/yr, 1,000 AI credits). — [OutlierKit comparison](https://outlierkit.com/resources/1of10-alternatives/) (competitor-authored, treat with care); [toolsurf review](https://www.toolsurf.com/1-of-10-2026/)
- vidIQ: free tier 150 AI credits/month; Boost ~$16.58–25/mo (annual); Max $39/mo (annual); daily ideas feed. — [OutlierKit](https://outlierkit.com/resources/1of10-alternatives/)
- ViewStats (co-founded by MrBeast): Chrome extension overlays view trajectories, outlier scores, thumbnail history; free tier, Pro $49.99/mo, $479.88/yr. — [OutlierKit](https://outlierkit.com/resources/viewstats-chrome-extension/)
- Other outlier tools: OutlierKit, NexLev, Spotter Studio, TubeBuddy, Social Blade, TubeLab. — [OutlierKit](https://outlierkit.com/resources/1of10-alternatives/); [TubeLab](https://tubelab.net/blog/5-alternatives-to-1of10)
- n8n templates use "custom virality score" + AI scoring against channel history, storing in Google Sheets/Airtable. — [n8n #7923](https://n8n.io/workflows/7923-create-viral-youtube-content-from-reddit-posts-with-gpt-4o-and-google-sheets/); [n8n #15253](https://n8n.io/workflows/15253-score-daily-viral-youtube-shorts-ideas-using-reddit-rss-and-deepseek-ai/)
- last30days ranks by real engagement (Reddit upvotes, top comments, Polymarket odds) rather than search-engine ranking. — [GitHub](https://github.com/mvanhorn/last30days-skill)

### Inferences
- DIY outlier score is trivially computable from yt-dlp metadata: for each tracked channel keep last N=30 videos, `outlier = views / median(views)`, normalized for age (views at day 7). Flag ≥3x. This replicates the paid tools for a curated list of ~30–100 vibe-coding channels at zero cost.
- Suggested composite score (0–100): 35% engagement outlier/velocity, 20% cross-source cluster size (embedding clustering, e.g., cosine > 0.8), 25% LLM niche-fit/novelty vs. existing backlog (dedupe by embedding), 20% "evergreen/search demand" (Google Trends/keyword volume). Store in Postgres with pgvector (dedupe/clustering) or Airtable/Notion for manual triage; Obsidian works if Claude Code is the main agent.

### Gaps
- No independent data validating that outlier scores predict performance for a *blog* (as opposed to YouTube). Google Trends official API status not verified (pytrends archived).

## 4. X/Twitter data access cost and scraping alternatives/risks

### Takeaway
As of Sept 2026, X's official API is **pay-per-use** by default for new developers: ~$0.005 per post read (cap 3M reads/billing cycle), $0.010 per user read; no Free/Basic/Pro tier for new signups (per multiple 2026 secondary sources — official docs.x.com blocked in this session, verify). Monitoring 50 accounts × 10 posts/day ≈ 15k reads/month ≈ $75/month officially vs ≈ $6/month via Apify ($0.40/1k). Scraping is cheaper but violates X ToS and needs burner accounts/proxies.

### Cited Findings
- Pay-per-use: $0.005/post read, capped at 3M post reads per billing cycle; $0.010/user read; $0.015 to create a post; $0.20 for a post with URL; prepaid credits, no subscription or minimum; "as of September 2026 there is no Free, Basic or Pro tier for anyone signing up". — [scrapecreators blog](https://scrapecreators.com/blog/twitter-pay-per-use-api); [outstand.so](https://www.outstand.so/blog/x-api-pricing); [twitterapi.io](https://twitterapi.io/blog/x-api-cost-breakdown-2026); [sorsa](https://api.sorsa.io/blog/twitter-api-pricing-2026) (all secondary, several are competitor vendors; official page docs.x.com/x-api/getting-started/pricing was not reachable)
- Apify apidojo Tweet Scraper V2: $0.40 / 1,000 tweets. — [Apify](https://apify.com/apidojo/tweet-scraper)
- Third-party paid X APIs exist (twitterapi.io, Sorsa, ScrapeCreators) marketing themselves as cheaper than official. — [twitterapi.io](https://twitterapi.io/blog/x-api-cost-breakdown-2026); [scrapecreators](https://scrapecreators.com/blog/twitter-pay-per-use-api)
- Open-source scrapers: twikit (4.7k stars), twscrape (2.8k, multi-account rotation). Nitter is archived. — [twikit](https://github.com/d60/twikit); [twscrape](https://github.com/vladkens/twscrape); [nitter](https://github.com/zedeus/nitter)
- last30days supports X via official API credits, browser cookies, or third-party keys. — [GitHub](https://github.com/mvanhorn/last30days-skill)

**Related: Reddit access in 2026 (similar story)**
- Reddit's Responsible Builder Policy (Nov 2025) gates all new API access behind manual approval; "create app" routes to a Data Access Request, reviewed by a human, replies in ~2–4 weeks, small projects frequently rejected. — [Reddit Help](https://support.reddithelp.com/hc/en-us/articles/42728983564564-Responsible-Builder-Policy); [fetchlayer](https://fetchlayer.dev/blog/reddit-api-closed-2026); [postwire](https://postwire.io/platforms/reddit/approval/)
- Unauthenticated `.json` returns 403 in 2026; `https://www.reddit.com/r/<sub>/new/.rss` still returns 200. — [DEV Community](https://dev.to/listwright/reddits-json-returns-403-in-2026-the-rss-feeds-still-answer-1gg5)
- Since June 2026 many Reddit RSS feeds return 429 (IP-based rate limit); workaround: add `user=` and `feed=` params from your account's RSS preferences (private feed token). Reddit has called RSS "another common surface for scraping". — [lapcatsoftware](https://lapcatsoftware.com/articles/2026/6/3.html); [DEV Community](https://dev.to/listwright/reddits-json-returns-403-in-2026-the-rss-feeds-still-answer-1gg5)

### Inferences
- For a solo creator: X via Apify or a list of accounts through RSSHub with a burner account cookie; never scrape with your main brand account (ban risk). Reddit via authenticated-token RSS (low volume, ~10–20 subreddits hourly) is the cheapest safe option.

### Gaps
- Official X pricing page not fetched (egress block); enterprise pricing and whether legacy Basic ($200/mo) / Pro ($5,000/mo) subscribers are grandfathered not confirmed.
- Legal/ToS risk specifics of twikit/twscrape account bans not quantified.

## 5. Best sources for the vibe-coding niche

### Takeaway
Core monitoring list: subreddits r/vibecoding, r/ClaudeAI, r/cursor, r/ChatGPTCoding, r/LLMDevs, r/SideProject, r/indiehackers; Discords of Lovable (~170k), Bolt.new (~95k), r/vibecoding (~8k); YouTube creators Greg Isenberg, Riley Brown, Theo (t3.gg), ThePrimeagen; plus official changelogs (tracked via changedetection.io) and GitHub Trending.

### Cited Findings
- Subreddits: r/ClaudeAI, r/LLMDevs, r/ChatGPTCoding, r/githubcopilot; r/vibecoding (89,000+ members), r/VibeCodeDevs (15,000+), r/SideProject (200,000+), r/indiehackers (150,000+). — [aitooldiscovery](https://www.aitooldiscovery.com/guides/vibe-coding-reddit); [Hive Index](https://thehiveindex.com/topics/vibe-coding/platform/reddit/)
- Discords: vibecoding Discord (official r/vibecoding, ~8K), Lovable Discord (~170K), Bolt.new Discord (~95K). — [Hive Index](https://thehiveindex.com/topics/vibe-coding/)
- Creators: Greg Isenberg (product/AI workflow ideas), Riley Brown (fast shipping), Cody Schneider (distribution), Vibe Coding Studio (agent workflows), freeCodeCamp, Theo – t3.gg (tool opinions), ThePrimeagen (stress-testing). — [daily.dev blog](https://daily.dev/blog/best-content-for-vibe-coders/)
- Newsletters: The Pragmatic Engineer, ByteByteGo, TLDR Web Dev, JavaScript Weekly, plus "A Vibe Coder"-type newsletters (InboxReads lists 25 similar). — [thectoclub](https://thectoclub.com/career/best-coding-newsletters/); [InboxReads](https://inboxreads.co/like/a-vibe-coder)
- daily.dev itself is tagged "vibe-coding-friendly" and aggregates dev news. — [GitHub](https://github.com/dailydotdev/daily)
- Techmeme and HN are included by last30days as free tech-news layers. — [GitHub](https://github.com/mvanhorn/last30days-skill)

### Inferences
- Add (from domain knowledge, not verified this session): official changelogs/blogs of Anthropic (Claude Code release notes on GitHub `anthropics/claude-code` releases → Atom feed), Cursor changelog, OpenAI Codex, Lovable, Bolt, v0, Replit; GitHub topic searches (`claude-code`, `mcp`, `vibe-coding`) sorted by stars created in last 7 days; HN Algolia keyword alerts for "Claude Code", "Cursor", "vibe coding"; Simon Willison's blog; Latent Space; Ben's Bites; Every (Dan Shipper); YouTube channels IndyDevDan, AI Jason, Cole Medin, Matthew Berman. Treat as candidates to validate.
- For Russian-language audience, add Telegram channels via RSSHub `/telegram/channel/<name>` route (prior knowledge).

### Gaps
- Member counts come from directory sites (Hive Index, aitooldiscovery), not Reddit itself; could not verify current numbers. No authoritative ranking of vibe-coding YouTube channels by subscribers found. Russian-language Telegram channels for vibe coding not researched.
