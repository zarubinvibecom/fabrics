# Multi-platform publishing / cross-posting infrastructure (Western + RU platforms), state as of Sept 2026

Methodological note: official doc domains (docs.x.com, developers.google.com, habr.com) were blocked by the research proxy, so several API facts below come from third-party vendor blogs (Blotato, upload-post, Outstand, Postproxy, Zernio, bundle.social) that sell competing unified APIs. Treat these as "likely accurate but verify against official docs before building". GitHub star counts were pulled live via GitHub API on 2026-09-30.

## 1. Open-source schedulers (Postiz, Mixpost, Socioboard, others)

### Takeaway
Postiz is by far the dominant open-source scheduler (~36.5k stars, AGPL-3.0, 30+ platforms incl. Telegram, Reddit, Bluesky, Mastodon), with Mixpost (~3.7k stars, Laravel, lighter stack) as the main alternative; newer AGPL projects (Brightbean Studio, TryPost) appeared in 2026. None of them solves the Russian long-form platforms (Dzen/Habr/VC.ru/Rutube) — those need custom code.

### Cited Findings
- gitroomhq/postiz-app: 36,540 stars, 7,042 forks, 241 open issues, TypeScript/Next.js, active (updated 2026-09-30); companion repo gitroomhq/postiz-agent (499 stars, created Feb 2026) is a CLI for connecting Postiz to Claude/other agents — [GitHub search API](https://github.com/gitroomhq/postiz-app), [postiz-agent](https://github.com/gitroomhq/postiz-agent)
- Postiz is AGPL-3.0, self-hosted version has no feature limitations vs cloud; supports X, LinkedIn, Instagram, Facebook, TikTok, YouTube, Threads, Pinterest, Reddit, Discord, Bluesky, Mastodon, Telegram, Slack, Google Business etc. ("34 platforms" per its posting-rules docs) — [Railway template](https://railway.com/deploy/postiz-self-hosted-buffer-alternative-for-30-platforms--postiz-social-scheduler), [Postiz docs](https://docs.postiz.com/general/quickstart)
- Postiz Cloud pricing from $29/month (with AI agents, MCP and API) — [Postiz pricing](https://postiz.com/pricing)
- Postiz uses a Temporal-based stack (heavier to self-host); Mixpost is a lighter Laravel stack, with a free "Lite" edition and paid self-hosted licenses "from $299 one-time", no AGPL network-copyleft obligation; Mixpost has thinner AI features and smaller community. Note: source is a competitor (Blotato) blog — [Blotato: Postiz alternatives](https://www.blotato.com/blog/postiz-alternatives)
- Self-hosting caveat: with self-hosted tools you "own uptime, updates, and OAuth breakage" — i.e. you must register your own developer apps on every platform (Meta, TikTok, Google, LinkedIn, X) and pass their reviews yourself — [Blotato: Postiz alternatives](https://www.blotato.com/blog/postiz-alternatives)
- inovector/mixpost: 3,747 stars, Vue/Laravel, 36 open issues, active — [GitHub](https://github.com/inovector/mixpost)
- Socioboard-developers/Socioboard-5.0: 1,513 stars, 37 open issues, created 2016; still updated but a legacy project with narrow focus (topics: LinkedIn, Twitter) — [GitHub](https://github.com/Socioboard-developers/Socioboard-5.0)
- New 2026 entrants: brightbeanxyz/brightbean-studio (2,392 stars, AGPL-3.0, Django/HTMX, "10+ platforms", created Mar 2026); trypostit/trypost (662 stars, AGPL-3.0, Laravel/Vue, created Jan 2026, topics include TikTok, YouTube, Threads, Pinterest); Anil-matcha/Free-AI-Social-Media-Scheduler (529 stars, MIT) — [brightbean-studio](https://github.com/brightbeanxyz/brightbean-studio), [trypost](https://github.com/trypostit/trypost), [Free-AI-Social-Media-Scheduler](https://github.com/Anil-matcha/Free-AI-Social-Media-Scheduler)
- A self-hoster's write-up: "Self-Hosting Postiz on RHEL 10: One Container, Six Platforms" — indicates realistic personal setups connect a subset of platforms — [crunchtools](https://crunchtools.com/self-hosting-postiz-rhel10-one-container-six-platforms/)

### Inferences
- For a solo creator, Postiz self-hosted is the most complete free option, but the real effort is not Docker — it's registering and getting approved on each platform's developer program (TikTok audit, Meta app review, Google YouTube audit, X paid API). A hosted Postiz/unified API bypasses this because it uses the vendor's already-audited apps.
- 241 open issues on Postiz suggests integration breakages are common (platform API churn); plan for periodic re-auth/maintenance.

### Gaps
- Could not verify the exact current Postiz provider list for VK specifically (not confirmed in fetched sources) — check Postiz docs/providers folder.
- No first-hand Reddit (r/selfhosted) threads were retrieved; search results returned only vendor/aggregator pages. Real-world bug reports should be checked in Postiz GitHub issues.

## 2. Unified posting APIs / SaaS (Ayrshare, upload-post, Late/Zernio, Blotato, Buffer, Publer, Metricool, Hootsuite, Typefully)

### Takeaway
Developer-oriented unified APIs range from ~$0 (free tiers) to $149+/mo; Late has rebranded to Zernio with per-account pricing; upload-post is the cheapest API with a free tier. Consumer schedulers (Buffer, Publer) are ~$4–6 per channel/month; Typefully is text-only (X/LinkedIn/Threads/Bluesky/Mastodon). None of them natively cover Dzen/Habr/VC.ru/Rutube.

### Cited Findings
- Ayrshare: Premium $149/mo (1 profile, up to 14 social accounts), Launch $299/mo, Business from $599/mo — [upload-post: Ayrshare pricing](https://www.upload-post.com/ayrshare-pricing/) (competitor source); described as "category incumbent but expensive at scale", pure API with no end-user dashboard — [Zernio: unified API](https://zernio.com/blog/unified-social-media-api)
- upload-post.com: free plan 10 uploads/month forever, no card; cheapest paid plan $24/mo ($16/mo annually) with unlimited posts; hosted MCP server with 40 tools — [upload-post pricing comparison](https://www.upload-post.com/pricing-comparison/) (self-reported)
- Late (getlate.dev) is now "Zernio": first 2 accounts free, then $6/account/mo (3–10), $3 (11–100), $1 (101+); 16 channels incl. posting, comments, DMs, analytics, ads — [Blotato: Ayrshare alternatives](https://www.blotato.com/blog/ayrshare-alternatives), [Zernio](https://zernio.com/blog/unified-social-media-api)
- Blotato: official n8n and Make nodes; publishes to Instagram, YouTube, TikTok, Facebook, LinkedIn, Threads, X, Pinterest, Bluesky (9 platforms); API access is a paid feature — [n8n workflow 3522](https://n8n.io/workflows/3522-auto-publish-social-videos-to-9-platforms-via-google-sheets-and-blotato/), [sabrina.dev](https://www.sabrina.dev/p/easy-social-media-posting-n8n-make)
- bundle.social: unified API for publishing, scheduling, analytics, comments and webhooks across 15 platforms — [bundle.social](https://bundle.social/unified-social-media-api)
- Buffer: Essentials $5/channel, Team $10/channel; supports Instagram, Facebook, X, LinkedIn, Pinterest, TikTok, YouTube, Bluesky, Threads, Mastodon — [Zapier roundup / search summary](https://zapier.com/blog/best-social-media-management-tools/), [usecarly](https://www.usecarly.com/blog/buffer-alternatives/)
- Publer: $5/mo first account + $4/mo each additional (every 10th free); covers Facebook, Instagram, TikTok, X, Threads, LinkedIn, Pinterest, Mastodon, Google Business, YouTube, Telegram, Bluesky, WordPress — [eden.so](https://eden.so/blog/buffer-alternatives/)
- Metricool: free plan; Starter from $25/mo, Advanced from $67/mo; does not support Bluesky/Mastodon (per comparison) — [socialk.it](https://socialk.it/en/compare/buffer-vs-metricool), [postplanify](https://postplanify.com/compare/buffer-vs-metricool)
- Typefully: free 15 posts/month; from $10/month; text-first for X, LinkedIn, Threads, Bluesky, Mastodon — [xposterai](https://xposterai.com/blog/buffer-alternatives-2026)
- Hootsuite: no current price retrieved (gap).
- RU-market SaaS: Postmypost claims official Rutube API integration for videos and Shorts — [postmypost.io/rutube](https://postmypost.io/rutube/)

### Inferences
- Cost-effective stack for a solo creator: upload-post or Zernio (API, video-heavy, cheap) for Western platforms + own scripts for RU platforms; or Postmypost (RU SaaS) if Rutube/VK/Dzen in one UI matters.
- Payment from Russia: Western SaaS (Buffer, Ayrshare, etc.) generally require non-Russian cards due to sanctions — needs a foreign card / intermediary (inference; not specifically sourced).

### Gaps
- Hootsuite 2026 pricing not retrieved. Blotato's own subscription prices not retrieved.
- No source confirming which Western SaaS accept Russian payments or block RU IPs.

## 3. Official API realities per platform

### Takeaway
Every major Western platform now has an official posting path, but with gates: YouTube and TikTok force private visibility until an audit; Instagram requires professional account; X is pay-per-use ($0.015/post, $0.20 with link); LinkedIn personal posting is self-serve; Threads/Bluesky/Mastodon are free and permissive. RU: VK and Telegram have full APIs; Rutube has an OAuth API (used by Postmypost); Dzen has no open API (workaround via Telegram bot sync); Habr and VC.ru have no public write API (browser automation or undocumented internal API only).

### Cited Findings
**YouTube (long + Shorts)**
- Default quota 10,000 units/day per Google Cloud project; extensions only via the YouTube API Services Audit and Quota Extension Form (manual review) — [upload-post YouTube API guide](https://www.upload-post.com/youtube-api/), [channelcrawler](https://channelcrawler.com/insights/youtube-api-daily-limit-quotas-costs-and-how-to-scale-beyond-10000-units-channelcrawler)
- videos.insert historically cost 1,600 units (≈6 uploads/day on default quota). Vendor sources claim Google cut it to ~100 units on 4 Dec 2025, and since 1 June 2026 videos.insert bills to its own bucket at 1 unit/call capped at 100 calls/day. UNVERIFIED against Google's docs (developers.google.com blocked) — flag as possibly inaccurate — [Blotato YouTube API pricing](https://www.blotato.com/blog/youtube-api-pricing), [socialcrawl](https://www.socialcrawl.dev/blog/youtube-data-api-2026)
- Uploads from unverified API projects created after 28 July 2020 are locked to private until the project passes the YouTube API Services audit — [growati / search summary](https://growati.com/blogs/youtube-api-quota-guide); official method page: [Videos: insert](https://developers.google.com/youtube/v3/docs/videos/insert)
- Shorts: uploaded via the same videos.insert (vertical ≤ 3 min is auto-classified) — general knowledge, not re-verified.

**TikTok**
- Unaudited Content Posting API clients: posts only SELF_ONLY (private), max 5 users posting per 24h, and the posting account must itself be private; error `unaudited_client_can_only_post_to_private_accounts` — [Outstand](https://www.outstand.so/blog/tiktok-content-posting-api), [bulkpublish](https://www.bulkpublish.com/blog/tiktok-content-posting-api/), [fablepeak PR](https://github.com/ttropolis/fablepeak/pull/30)
- "Upload to inbox" (draft sent to creator's app, finish manually) needs no audit; Direct Post needs audit for public visibility — [vorplabs](https://vorplabs.com/agent-tools/tiktok-content-posting-api)
- Audit approval/rejection realities — [bundle.social](https://bundle.social/blog/tiktok-api-approval)

**Instagram (Reels/posts/carousels) / Facebook**
- Requires professional (business/creator) account via Instagram Platform content publishing; limit now 100 API-published posts per 24h moving window (Reels, images, carousels, stories all count; carousel = 1). Older doc field still says 50 — check `GET /<IG_ID>/content_publishing_limit` — [Meta docs](https://developers.facebook.com/docs/instagram-platform/content-publishing/), [bundle.social](https://bundle.social/blog/instagram-api-rate-limits), [postproxy](https://postproxy.dev/blog/instagram-reels-api-publishing-guide/)

**Threads**
- 250 API-published posts per 24h moving window; carousel = 1 — [Meta Threads API overview](https://developers.facebook.com/documentation/threads/overview), [Blotato Threads pricing](https://www.blotato.com/blog/threads-api-pricing)

**X/Twitter**
- Since 6 Feb 2026 pay-per-use is the default, no free tier for new developers; $0.015 per post created, $0.20 if the post contains a URL; summoned reply $0.010 — [X pricing docs](https://docs.x.com/x-api/getting-started/pricing) (via search snippet), [postproxy](https://postproxy.dev/blog/x-api-pricing-2026/), [postzen](https://www.postzen.dev/blog/twitter-api-pricing)

**LinkedIn**
- Posting to your own profile: self-serve "Share on LinkedIn" product gives `w_member_social` without review. Company pages / posting on behalf of others / analytics require Community Management API (partner application, weeks to months, opaque rejections) — [Blotato LinkedIn API](https://www.blotato.com/blog/linkedin-posting-api), [bundle.social](https://bundle.social/blog/linkedin-api-post-profiles-company-pages), [Phyllo](https://www.getphyllo.com/post/linkedin-api-access-in-2026-partner-program-approval-timeline-alternatives)

**Bluesky**
- AT Protocol, free; write limit 5,000 points/hour and 35,000/day, CREATE = 3 points (≈1,666 records/hour, 11,666/day) — [Blotato rate limits](https://www.blotato.com/blog/social-media-api-rate-limits)

**Medium / Substack / dev.to / Hashnode**
- Medium stopped issuing new integration tokens and new integrations (as of 1 Jan 2025); existing tokens still work; API unsupported. Medium's Import tool sets canonical automatically — [Medium help](https://help.medium.com/hc/en-us/articles/213480228-API-Importing), [medium-publishing-without-api](https://github.com/iancarson/medium-publishing-without-api), [Make community](https://community.make.com/t/integration-token-issue-with-medium-com/64777)
- dev.to REST API supports `canonical_url`; Hashnode GraphQL supports `originalArticleURL` — [dev.to syndication](https://dev.to/navinvarma/blog-syndication-cross-publishing-blog-posts-to-devto-hashnode-and-medium-1a5d)
- Substack: no public posting API found in sources (gap below).

**Telegram**
- Bot API: bots upload up to 50 MB and download up to 20 MB; self-hosted local Bot API server (open-source C++) allows uploads up to 2000 MB — [Telegram Bot API](https://core.telegram.org/bots/api), [bigmike.help](https://bigmike.help/en/devops/local-telegram-bot-api-advantages-limitations-of-the-standard-api-and-set-eb4a3b/)

**VK / VK Video / Clips**
- Official VK API supports wall posting and video upload (video.save → upload URL, video.addAlbum etc.); in 2026 VK moved to API v5.230+ with event-driven emphasis — [Habr VK autoposting](https://habr.com/ru/articles/657569/), [codeby](https://codeby.net/threads/zagruzhayem-video-v-pleilisty-vk-s-pomoshch-yu-vk-api-i-python.81862/), [mayai.ru](https://mayai.ru/vk-api-avtomatizacziya-postov-lidov-i-uvedomlenij-cherez-make-v-2026/)

**Rutube**
- OAuth 2.0 upload API exists (per integrators); Postmypost markets an "official Rutube API" integration for video and Shorts; Rutube also launched a "video showcase" embed API — [postmypost](https://postmypost.io/rutube/), [work-zilla](https://work-zilla.com/development-and-it/api-integrations/loading-video-through-rutube-api), [Telesputnik](https://telesputnik.ru/materials/video-novosti/news/rutube-predstavlyaet-novuyu-razrabotku-api-videovitrin)

**Dzen**
- Public API not accessible to regular users (bureaucratic registration); workaround: token from Dzen Studio settings + @zen_sync_bot to sync Telegram channel posts (text and video) into Dzen — [allslava.com](https://allslava.com/avtopostingh-v-dzien-v-2026-ghodu-kak-ia-nastroil-biesshovnuiu-voronku-kontienta-iz-telegram/); open-source TG→VK/Threads/Dzen autoposter — [asya-social-autopost](https://github.com/anomnia/asya-social-autopost)

**Habr / VC.ru**
- Habr: no API for publishing, only web editor; first article goes through the sandbox (moderation) — [Habr Sept 2026 article (via search snippet)](https://habr.com/ru/articles/1085322/)
- VC.ru: no official public write API; an internal admin API exists and enthusiasts document it for autoposting on vc.ru/dtf.ru; companies have used headless-browser robots — [DTF post on vc/dtf API](https://dtf.ru/id2850634/3819420-api-dlya-avtopostinga-na-vc-ru-i-dtf-ru), [vc.ru: automate without API](https://vc.ru/marketing/786357-kak-avtomatizirovat-bez-api), [Selectel on Habr](https://habr.com/ru/companies/selectel/articles/747494/). Sources conflict on whether any usable write API exists — treat internal API as unofficial and fragile.

### Inferences
- A TG-first workflow for RU (Telegram channel → Dzen via zen_sync_bot, → VK via API) is the lowest-effort RU path. Habr should remain manual (sandbox moderation + high community sensitivity to automated content).
- X at $0.20/link-post makes link-heavy auto-posting noticeably costlier; post the link in a reply or use text-only.

### Gaps
- Pinterest API (v5) and Reddit API posting rules/limits were not researched in this pass — Reddit is known to be hostile to self-promotion; verify separately.
- Mastodon: no source retrieved (generally open REST API per instance; instance rules vary).
- Substack: no confirmed public posting API; email newsletter tools (Buttondown, Ghost, Beehiiv, Unisender for RU) not researched.
- YouTube quota change claim needs confirmation from Google's official quota page.

## 4. Browser-automation fallbacks and ban risks

### Takeaway
Browser automation (Playwright/Selenium, dreammis/social-auto-upload) is widely used, especially in the Chinese ecosystem, but TikTok/Instagram detect missing human behavioral signals and device fingerprints; official APIs and approved schedulers do not cause shadowbans, while browser automation is a common trigger.

### Cited Findings
- dreammis/social-auto-upload: 15,262 stars, Python, uploads to Douyin, Xiaohongshu, WeChat Channels, TikTok, YouTube, Bilibili; web-UI fork DevilJie/social-auto-upload-web-ui (293 stars, May 2026) — [GitHub](https://github.com/dreammis/social-auto-upload), [web-ui](https://github.com/DevilJie/social-auto-upload-web-ui)
- TikTok client-side SDK collects behavioral signals (typing cadence, scroll, in-app navigation); uploads via unofficial APIs or browser automation lack them — [conbersa](https://www.conbersa.ai/learn/what-triggers-tiktok-shadowban-automation)
- TikTok analyzes device fingerprint, browser signatures, IP/ASN, timezone/geo, WebRTC leaks, cookies — [dev.to antidetect](https://dev.to/vietnam/best-antidetect-browsers-for-tiktok-multiple-accounts-jch)
- "Scheduling through an officially partnered tool that uses the platform APIs does not cause shadowbans… what does cause problems is browser automation, fake-engagement bots, and copy-paste posting across many accounts" — [mallary.ai](https://mallary.ai/blog/am-i-shadowbanned), [openhosst](https://openhosst.com/blog/tiktok-automation)
- VC.ru/Habr automations have historically used headless browsers mimicking humans — [vc.ru](https://vc.ru/marketing/786357-kak-avtomatizirovat-bez-api)

### Inferences
- Use browser automation only where no API exists (Habr, VC.ru, possibly Dzen long-reads), at low frequency, from a stable residential IP and persistent logged-in profile; never for TikTok/Instagram where official paths exist.
- Geo: accessing TikTok/Instagram/Facebook/X from Russia requires VPN (these are blocked/restricted in RU); IP/geo mismatches are a fingerprint signal — run the Western-platform publisher on a foreign VPS (inference based on fingerprint signals above; RU blocking not re-sourced here).

### Gaps
- No quantitative ban-rate data found; evidence is vendor/blog-level.

## 5. Canonical / SEO when cross-posting articles (POSSE)

### Takeaway
POSSE (Publish on Own Site, Syndicate Elsewhere) is the standard: publish on own Astro/Hugo blog first, then syndicate to dev.to (`canonical_url`), Hashnode (`originalArticleURL`), Medium (Import tool sets canonical) so ranking credit flows back to the original.

### Cited Findings
- dev.to `canonical_url`, Hashnode `originalArticleURL`, Medium import sets canonical automatically (must use import to preserve it) — [dev.to/navinvarma](https://dev.to/navinvarma/blog-syndication-cross-publishing-blog-posts-to-devto-hashnode-and-medium-1a5d), [nvarma.com](https://www.nvarma.com/blog/2026-02-10-cross-publishing-blog-posts-devto-hashnode-medium)
- Without canonical, Google may rank the platform copy above the original — [dev.to/mk023](https://dev.to/mk023/cross-posting-to-devto-without-giving-away-your-seo-5gd), [mikebifulco.com](https://mikebifulco.com/posts/own-your-work-with-canonical-tags)
- POSSE method description — [dev.to/mrakdon](https://dev.to/mrakdon/the-posse-method-own-your-content-while-leveraging-devto-and-hashnode-1obd); canonical chain across dev.to/Hashnode/Bluesky — [dev.to/morinaga](https://dev.to/morinaga/how-i-implemented-the-canonical-url-chain-across-devto-hashnode-and-bluesky-50d)

### Inferences
- RU platforms (Habr, VC.ru, Dzen) don't expose canonical controls; for RU, either publish the platform-native version first (Habr often ranks better than a new blog in Yandex) or rewrite/adapt rather than duplicate. Unverified — no source on Yandex behaviour found.

### Gaps
- No source on canonical support on Habr/VC.ru/Dzen or Yandex duplicate-content handling.

## 6. Analytics aggregation for a feedback loop

### Takeaway
Unified APIs (Zernio, bundle.social, Ayrshare, Data365) expose cross-platform analytics endpoints; dashboards like Metricool aggregate for Western networks. RU platforms need direct VK/Telegram stats APIs plus scraping; no single tool covers all.

### Cited Findings
- bundle.social: publishing + analytics + comments + webhooks across 15 platforms — [bundle.social](https://bundle.social/)
- Zernio: posting, comments, DMs, analytics, ads in one bearer token across 16 channels — [Zernio](https://zernio.com/blog/unified-social-media-api)
- Data365: unified read access to Instagram, Twitter, Reddit, TikTok, LinkedIn — [cm-alliance](https://www.cm-alliance.com/cybersecurity-blog/top-5-social-media-api-for-data-collection-and-analytics-in-2026)
- LinkedIn analytics scopes require Community Management API approval — [Blotato LinkedIn](https://www.blotato.com/blog/linkedin-posting-api)
- Analytics API field reference — [bundle.social analytics guide](https://bundle.social/blog/social-media-analytics-api-guide), [mallary.ai](https://mallary.ai/blog/social-media-analytics-api)

### Inferences
- Feedback loop design: pull per-post metrics nightly from the unified API used for publishing + YouTube Analytics API + VK stats + Telegram (views on channel posts) into a single DB, keyed by a content ID shared across platforms.

### Gaps
- Metricool API availability/pricing not confirmed; Rutube/Dzen analytics API availability not found; TGStat (RU Telegram analytics) not researched.

## 7. Community (Reddit r/selfhosted, r/socialmedia, r/n8n) experiences

### Takeaway
Direct Reddit threads could not be retrieved; the visible n8n ecosystem shows heavy use of Blotato (and upload-post) as the posting backend in n8n templates, which suggests the "n8n + unified API" pattern is the community default for video fan-out.

### Cited Findings
- Multiple official n8n templates use Blotato to publish to 9 platforms from Google Sheets / AI video pipelines — [n8n 3522](https://n8n.io/workflows/3522-auto-publish-social-videos-to-9-platforms-via-google-sheets-and-blotato/), [n8n 7187](https://n8n.io/workflows/7187-automate-content-publishing-to-tiktok-youtube-instagram-facebook-via-blotato/), [n8n 5608 (Klap shorts)](https://n8n.io/workflows/5608-convert-youtube-videos-to-shorts-with-klap-and-auto-post-to-multiple-social-platforms/)
- Paid Gumroad n8n templates built on Blotato are sold widely — [gumroad example](https://aiwithapex.gumroad.com/l/blotato-automation)

### Inferences
- The search engine surfaced vendor SEO content heavily; many "comparison" articles are written by competitors (Blotato, upload-post, Zernio, postproxy) — bias risk in all price comparisons.

### Gaps
- No actual Reddit user reports retrieved (search did not surface reddit.com threads). Recommend manual review of r/selfhosted "Postiz" threads and Postiz GitHub issues.
