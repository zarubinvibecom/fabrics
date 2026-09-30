# AI text content production and repurposing pipelines (vibe-coding blog, EN + RU platforms), state as of Sept 2026

Method note: GitHub star counts were pulled live on 2026-09-30 via the GitHub search API (the repo URLs are the sources). Several vendor/review pages (habr.com, apepublish.com, socialrails.com, buildmvpfast.com) were blocked by the egress proxy, so some claims below rely on search-result snippets rather than full-page reads. Those are flagged as such.

## 1. Open-source repos (research agents, writers, repurposers, anti-slop, publishers)

### Takeaway
No single mature OSS "content factory" stands out. The practical stack is a combination of pieces: a deep-research agent (STORM / GPT-Researcher), an orchestration layer (n8n, LangGraph or CrewAI, or Claude Code with Skills), an anti-slop skill (blader/humanizer, conorbronsdon/avoid-ai-writing), and a scheduler/publisher (Postiz). The dedicated "content repurposing" repos are small or aimed at video.

### Cited Findings
Star counts are as of 2026-09-30.
- **n8n-io/n8n**: about 206k stars, fair-code workflow automation with native AI and MCP client/server, 400+ integrations. This is the de facto no-code orchestration layer for content pipelines. — [GitHub](https://github.com/n8n-io/n8n)
- **Zie619/n8n-workflows**: about 56.9k stars, a large dump of n8n workflows that includes content and social templates. — [GitHub](https://github.com/Zie619/n8n-workflows)
- **anthropics/skills**: about 179k stars, the public Agent Skills repo from Anthropic (created Sept 2025). This is the base format for Claude Code writing skills. — [GitHub](https://github.com/anthropics/skills)
- **hesreallyhim/awesome-claude-code** (about 54.8k stars) and **travisvn/awesome-claude-skills** (about 15.2k stars) are the awesome lists where writing and content skills are catalogued. — [GitHub](https://github.com/hesreallyhim/awesome-claude-code), [GitHub](https://github.com/travisvn/awesome-claude-skills)
- **blader/humanizer**: about 53.1k stars, created Jan 2026. It is an "Agent skill that removes signs of AI-generated writing from text" and works with Claude Code, Codex and Cursor. It is the most popular anti-slop skill. — [GitHub](https://github.com/blader/humanizer)
- **conorbronsdon/avoid-ai-writing**: about 4.8k stars, created Mar 2026. It is a skill that "audits and rewrites content to remove AI writing patterns" and supports Claude Code, Codex, OpenClaw and Hermes. — [GitHub](https://github.com/conorbronsdon/avoid-ai-writing)
- **sam-paech/antislop-sampler**: about 354 stars. It suppresses slop phrases at the sampling level, which is only usable with local or open-weights models. — [GitHub](https://github.com/sam-paech/antislop-sampler)
- **stanford-oval/storm**: about 31.5k stars. An "LLM-powered knowledge curation system that researches a topic and generates a full-length report with citations" (EMNLP/NAACL paper). It is a good fit for Wikipedia-style long-read drafts. — [GitHub](https://github.com/stanford-oval/storm)
- **assafelovic/gpt-researcher**: about 29.8k stars, an autonomous deep-research agent that works with any LLM and has an MCP server. — [GitHub](https://github.com/assafelovic/gpt-researcher)
- **dzhng/deep-research**: about 19.7k stars, a minimal deep-research agent in TypeScript. — [GitHub](https://github.com/dzhng/deep-research)
- **langchain-ai/open_deep_research**: about 12.7k stars, now **archived**. — [GitHub](https://github.com/langchain-ai/open_deep_research)
- **crewAIInc/crewAI** (about 59.2k stars) and **langchain-ai/langgraph** (about 42.5k stars) are the multi-agent frameworks. Researcher→writer→editor "content crew" examples are built on them. — [GitHub](https://github.com/crewAIInc/crewAI), [GitHub](https://github.com/langchain-ai/langgraph)
- **langchain-ai/social-media-agent**: about 2.8k stars. "An agent for sourcing, curating, and scheduling social media posts with human-in-the-loop." This is the closest official reference architecture for turning a URL into drafted posts, then human approval, then scheduling. — [GitHub](https://github.com/langchain-ai/social-media-agent)
- **gitroomhq/postiz-app**: about 36.5k stars, an open-source "agentic social media scheduling tool" that can be self-hosted. It is the OSS alternative to Buffer/Typefully. — [GitHub](https://github.com/gitroomhq/postiz-app)
- **zarazhangrui/follow-builders**: about 6.8k stars. It monitors AI builders on X and on YouTube podcasts and "remixes their content into digestible summaries", which is a useful pattern for a curated vibe-coding digest. — [GitHub](https://github.com/zarazhangrui/follow-builders)
- **JimmyLv/BibiGPT-v1**: about 6.2k stars. It gives one-click summaries of YouTube, podcasts and other audio/video, which fits source ingestion for repurposing. — [GitHub](https://github.com/JimmyLv/BibiGPT-v1)
- **yaojingang/GEOFlow**: about 3.7k stars. A "GEO content engineering and multi-site distribution platform with AI quality inspection". — [GitHub](https://github.com/yaojingang/GEOFlow)
- Video-side repurposers: **harry0703/MoneyPrinterTurbo** (about 127k stars, topic to short video) and **RayVentura/ShortGPT** (about 8k stars). — [GitHub](https://github.com/harry0703/MoneyPrinterTurbo), [GitHub](https://github.com/RayVentura/ShortGPT)
- Image and code-screenshot tooling: **vercel/satori** (about 14k stars, HTML/CSS/JSX to SVG, used for OG images and carousels), **carbon-app/carbon** (about 36.1k stars, code images) and **raycast/ray-so** (about 2.4k stars, code snippet images). — [GitHub](https://github.com/vercel/satori), [GitHub](https://github.com/carbon-app/carbon), [GitHub](https://github.com/raycast/ray-so)

### Inferences
- A lean pipeline for this blog could look like this. Claude Code runs with a custom "voice" skill, which is style guide plus a corpus of your own posts. Research runs through GPT-Researcher or STORM. The humanizer or avoid-ai-writing skill does an audit pass. Postiz or Typefully's API/MCP handles X, Threads, LinkedIn and Bluesky. Custom scripts or bots handle Telegram, Habr, VC.ru and Dzen, where no OSS tool is dominant.
- Maturity: n8n, CrewAI, LangGraph, STORM and GPT-Researcher are mature and actively maintained (all were pushed within the last day). The skills (humanizer, avoid-ai-writing) are new (2026) but very popular. langchain social-media-agent is a reference example, not a product. open_deep_research is archived.
- Licenses were not returned by the API call. From prior knowledge, still unverified: n8n uses the Sustainable Use License (fair-code, not OSI). STORM, GPT-Researcher, CrewAI and LangGraph are MIT or Apache-2.0. Postiz is AGPL-3.0. Check before commercial use.

### Gaps
- I could not verify licenses or check markdown→multi-platform cross-posters (e.g. Wechatsync-style tools, dev.to/Hashnode/Medium CLI publishers, Habr/VC.ru auto-posters). A GitHub search for them returned 0 hits with my query syntax.
- I found no well-starred OSS tool that publishes to Habr, VC.ru or Dzen. These appear to need manual posting or custom browser automation, but I did not confirm this.

## 2. SaaS tools and prices

### Takeaway
Social-post SaaS is cheap: Typefully runs about $8–20 per social set per month. LinkedIn-focused Taplio runs $39–199 per month. Transcript-to-content tools (Castmagic) run about $21–295 per month. Pricing changes often and review sites disagree, so verify on vendor pages.

### Cited Findings
- **Typefully**: priced per "social set". Free: 1 set, 15 posts/month, and it includes agents/API/MCP access. Creator/Pro: $10/month monthly (about $8 annual). Business: $20/month (about $18 annual), with collaboration and teams. Enterprise is custom. — [aiproductivity.ai](https://aiproductivity.ai/pricing/typefully/), [toolradar](https://toolradar.com/tools/typefully/pricing) (from search snippets; the sources note inconsistencies)
- **Taplio** (LinkedIn): Starter $39/month (no AI credits). Standard $65/month (250 AI credits). Pro $199/month (5,000 AI credits, lead DB). — [coldiq](https://coldiq.com/blog/taplio-pricing) (search snippet)
- **Hypefury**: one snippet says it "changed in 2026 to no longer support X and now targets LinkedIn, Bluesky, Threads and Instagram, from $6/mo per channel". Another lists "Starter $29 · Creator $65 · Business $97 · Agency $199 (June 2026)". **These conflict.** — [socialrails](https://socialrails.com/blog/hypefury-pricing), [Taplio vs Hypefury](https://taplio.com/blog/taplio-vs-hypefury) (full page blocked)
- **Castmagic** (audio/video to content assets): sources conflict. One says Hobby $21/month (annual) and Starter $79/month (annual). Another says Free (3 files), Starter $39, Pro $99 and Business $295 (API). — [aisotools](https://aisotools.com/pricing/castmagic), [xpay](https://www.xpay.sh/saas-pricing/castmagic-io/)
- Justin Welsh's system uses Hypefury for scheduling the "spokes" cut from his newsletter. — [thinkdmg](https://thinkdmg.com/high-impact-low-time-investment-the-justin-welsh-content-system/)

### Inferences
- For a solo EN+RU creator, Typefully Free/Creator (whose API/MCP can be driven from Claude Code) or self-hosted Postiz covers X, Threads, LinkedIn and Bluesky. Paying for Jasper-class all-in-one writers is hard to justify when Claude/GPT subscriptions plus skills do the drafting.

### Gaps
- I did not verify current prices for Repurpose.io, Descript, Jasper, Opus Clip, Buffer or Publer, because the comparison page was blocked by the proxy.
- I did not research Russian SaaS (e.g. SMMplanner, Telegram scheduling bots, the VK/Dzen native schedulers).

## 3. Voice consistency, anti-slop, and platform policies on AI content

### Takeaway
Platforms mostly penalize generic, unedited output rather than AI use itself. The exception is Habr, which formally bans texts written or edited by neural networks under its 2026 rules. LinkedIn added a "Seems like AI slop" flag. Google targets scaled, unreviewed content. The defensible workflow is an AI draft, then human editing with specific personal details, then an anti-slop audit.

### Cited Findings
- **LinkedIn**: it added a "Seems like AI slop" option to the post menu. In May 2026 it announced "Keeping Conversations Real", which removed the AI writing assistant from the main compose button and pledged to downrank generic, automated-sounding content. — [switcherstudio](https://www.switcherstudio.com/whats-new/linkedin-ai-slop-button-creators), [Forbes, Aug 10 2026](https://www.forbes.com/sites/jodiecook/2026/08/10/what-linkedins-ai-slop-crackdown-means-for-your-posts/)
- LinkedIn data conflicts. One study of 8,695 posts found 14% carried AI markers and none were penalized. Other analyses claim "low-effort AI" posts get about 30% less reach and about 55% less engagement, and that fully AI posts get a 20–40% reach cut compared with hybrid posts. Another dataset shows AI-sounding posts getting 21% less engagement. — [cccrafts](https://cccrafts.ai/blog/does-linkedin-punish-ai-written-posts-2026), [zoomsphere](https://www.zoomsphere.com/blog/linkedin-algorithm-2026-why-generic-ai-content-kills-your-organic-reach), [ligosocial State of LinkedIn 2026 (134k posts)](https://ligosocial.com/research/state-of-linkedin-2026). The consensus across sources: hybrid posts (AI draft plus human edits plus specifics) perform like human posts.
- Pangram Labs scanned more than 1M posts that users scrolled past on LinkedIn, X, Reddit, Substack and Medium in 2026. LinkedIn has the highest rate of fully AI-written long-form content. — search summary referencing [technewsworld](https://www.technewsworld.com/story/linkedin-to-launch-campaign-against-ai-slop-180344.html) (not full-read)
- **Habr**: the "Новые правила Хабра. Версия от 2026" ban posting texts written or edited with neural networks, and Habr said it will hide generated content. — [Habr rules 2026](https://habr.com/ru/companies/habr/articles/1019036/) (search snippet; page blocked). Enforcement is weak. Moderators reportedly use free Russian detectors that return 0% AI on texts GPTZero rates 100% AI. — [dzen.guru](https://dzen.guru/news/neyroslop-na-khabre-nevidim-rossiyskie-detektory-dayut-0-gptzero-pokazyvaet-100), [Habr: «Хабр проиграл войну с нейрослопом»](https://habr.com/ru/articles/1081846/)
- **Russia, general**: Federal Law 243-FZ on AI was signed on July 26, 2026 and takes effect Sept 1, 2026. Platforms with 500k+ daily users must *give users the ability* to label AI-generated audio/visual material. This is an option, not a universal obligation for authors. A separate proposal (Aug 2026) would oblige users to label AI materials. — [kontur](https://talk.kontur-f.ru/news/zakon-ob-iskusstvennom-intellekte-i-markirovka-ii-kontenta/), [Vedomosti](https://www.vedomosti.ru/technology/articles/2026/08/18/1221812-polzovatelei-ii-predlozhili-obyazat-markirovat-sozdannie-neirosetyami-materiali), [CNews](https://www.cnews.ru/news/top/2026-08-18_polzovatelej_mogut_obyazat)
- **Dzen** reportedly requires no special marking for AI texts but lowers visibility of "raw" neural-network texts. — search summary ([dzen.guru rules](https://dzen.guru/blog/pravila-dzena-dlya-avtorov)). This is low confidence.
- **Google**: "appropriate use of AI or automation is not against our guidelines". "Scaled content abuse" (many pages made mainly to manipulate rankings) is penalized regardless of how it was made. Human review and oversight is the practical dividing line. A May 2026 extension applies spam policies to eligibility for AI Overviews and AI Mode citations. There were spam updates in Aug and Sept 2026. — [ppc.land](https://ppc.land/google-spam-policies-now-officially-cover-ai-overviews-and-ai-mode-in-search/), [postforsuccess](https://postforsuccess.com/scaled-content-abuse), [primotech](https://primotech.com/google-september-2026-spam-update/)
- **Reddit** positions itself as "provably human" through a campaign and blog post, rather than adding a flag button. — search summary ([technewsworld](https://www.technewsworld.com/story/linkedin-to-launch-campaign-against-ai-slop-180344.html))
- Anti-slop tooling exists as skills: humanizer and avoid-ai-writing (section 1).

### Inferences
- Voice-cloning best practice, synthesized:
  1. Keep a written style guide: tone, banned words and constructions, sentence rhythm, how you use RU vs EN terms.
  2. Keep a corpus of 10–30 of your best posts per platform as few-shot examples, in a Claude Project or skill.
  3. Always inject a "personal detail" slot: a real bug, real numbers, a screenshot from your own vibe-coding sessions.
  4. Run an anti-slop audit with humanizer or avoid-ai-writing before publishing.
  5. Make a human pass mandatory before publishing.
- For Habr, write personally and use AI only for research, outline and fact checks. Publishing AI-edited text violates the rules as written, even if enforcement is weak. That creates reputational risk in a dev-heavy audience that hunts for "нейрослоп".

### Gaps
- I did not verify X/Twitter's current stance on AI and automated posting, or the Threads and Bluesky policies.
- I did not directly sample Reddit threads (r/content_marketing, r/ClaudeAI, etc.). The creator-sentiment points above come from articles, not Reddit primary posts.
- VC.ru's AI-content rules were not found.

## 4. Pillar/atomization repurposing frameworks

### Takeaway
The proven pattern is one weekly pillar (newsletter, long post or video) cut into 6–30+ micro pieces. Welsh: 1 newsletter to 6–12 posts in about 4 hours a week. Koe: 1 newsletter to 1 thread plus 3 tweets a day. GaryVee: 1 keynote or podcast to 30+ (up to "64") pieces, plus a second round driven by community feedback.

### Cited Findings
- **GaryVee Content Model**:
  - Steps: pillar content, then micro content, then distribution, then community insights, then new community-driven micro content, then redistribution.
  - Yield: "30+ pieces" from one keynote, podcast or interview. A deck titled "How To Make 64 Pieces Of Content In A Day" also exists.
  - Sources: [GV Content Model PDF](https://s3.amazonaws.com/gv2016wp/wp-content/uploads/20180725172810/GV-Content-Model-1.pdf), [getgist](https://getgist.com/gary-vee-content-model/)
- **Justin Welsh, Content Operating System**:
  - Output: one newsletter plus 6–12 social posts per week for LinkedIn and X, in about 4 hours a week.
  - Method: the newsletter is "chopped" into observations, tips and lists, then scheduled via Hypefury.
  - Sources: [learn.justinwelsh.me](https://learn.justinwelsh.me/content), [thinkdmg](https://thinkdmg.com/how-justin-welsh-creates-a-weeks-worth-of-content-in-just-4-hours/)
  - Welsh also advocates building a "730-day content library" of evergreen posts to recycle. — [justinwelsh.me](https://www.justinwelsh.me/newsletter/build-a-content-library)
- **Dan Koe, 2 Hour Writer / content ecosystem**:
  - Cadence: 1 newsletter a week, archived on the blog. 1 thread a week derived from it. 3 tweets a day on the newsletter topic.
  - Direction: tweets are also turned *into* newsletters, so good short posts get expanded into pillars.
  - Sources: [econolearn substack](https://econolearn.substack.com/p/dan-koe-the-2-hour-writer), [startupanatomy](https://startupanatomy.substack.com/p/how-dan-koe-built-a-3m-one-person)

### Inferences
- A concrete weekly template for a vibe-coding blog, derived from the above and not from a source:
  - Pillar: one Habr, dev.to or Medium long-read, or one YouTube or screencast video.
  - From it, derive: 1 Substack/newsletter issue (EN) plus 1 Telegram long post (RU).
  - Also derive 1 X thread, 1 LinkedIn text post and 1 LinkedIn carousel (5–8 slides from satori or code screenshots), plus 1 VC.ru adaptation.
  - Add 5–7 short posts (X, Threads, Bluesky, Telegram) and 3–5 short-video scripts, for a total of about 15–20 assets per pillar.
- Use Koe's reverse loop: posts with high engagement become next week's pillar.

### Gaps
- I did not fetch the original GaryVee 64-piece deck for exact per-platform ratios.

## 5. LLMs for writing in 2026 and cost per piece

### Takeaway
Claude models lead creative/prose writing benchmarks as of Sept 2026. A full pillar plus ~15 derivative pieces costs well under $1–2 via API on Opus- or Sonnet-class models. A flat subscription (Claude Pro/Max, ChatGPT) is usually simpler for a solo creator.

### Cited Findings
- EQ-Bench Creative Writing leaderboard, Sept 2026: Claude Opus 5 is at #1 (Elo 2121), Kimi K3 at #2 (2071) and GPT-5.6 Sol at #3 (1963). Claude Fable 5.1 is reported to score best across 8 writing tests. — search summary citing [intellectualead](https://intellectualead.com/best-llm-writing/) and [buildmvpfast](https://www.buildmvpfast.com/articles/best-llms-2026-guide/content-writing-ai) (pages not fully read; treat as secondary)
- Lech Mazur's writing benchmark on GitHub tests incorporation of story elements. It is an alternative leaderboard. — [GitHub lechmazur/writing](https://github.com/lechmazur/writing)
- Anthropic API list prices, per 1M tokens input/output, from Anthropic's model table cached 2026-09-25 in the Claude API skill:

  | Model | Input $/1M | Output $/1M | Notes |
  |---|---|---|---|
  | Claude Fable 5.1 | $10 | $50 | |
  | Claude Opus 5.5 | $4 | $20 | |
  | Claude Opus 5 | $5 | $25 | |
  | Claude Sonnet 5.5 | $2 | $10 | |
  | Claude Haiku 4.5 | $1 | $5 | |
  | Batch API | | | 50% discount |

  — [Anthropic pricing docs](https://docs.anthropic.com/en/docs/about-claude/pricing)

### Inferences
- Example cost for one pillar article. Assume about 20k input tokens (sources, style guide, few-shot corpus) and about 4k output tokens, plus 2 revision rounds, for roughly 60k input and 12k output in total.
  - On Opus 5.5: about $0.24 input plus $0.24 output, so about $0.50.
  - On Sonnet 5.5: about $0.25.
- Atomizing into about 15 derivative pieces adds about 30k input and 10k output, which is about $0.30 on Opus 5.5.
- A pillar plus derivatives therefore lands in the ~$0.5–1 range on Opus 5.5 and roughly half that on Sonnet 5.5. Prompt caching of the style-guide prefix lowers it further.
- These are my estimates, not sourced figures.
- For Russian text, Claude and GPT write well. No benchmark on RU prose quality was found.

### Gaps
- I did not verify OpenAI GPT-5.x, Gemini 3.x or Kimi K3 API prices, or YandexGPT/GigaChat quality and pricing for Russian content.
- There is no benchmark of "slop score" by model in the sources I could read (EQ-Bench has one, but I did not fetch it).

## 6. Image generation for posts, thumbnails, carousels and code visuals

### Takeaway
For text-heavy thumbnails use Ideogram (about $0.03–0.10 per image) or GPT Image 2. For cheap photoreal/background images use FLUX.2 (from about $0.015). For carousels and OG cards use deterministic HTML→image (satori) plus code screenshots (Carbon, ray.so), which are free and on-brand.

### Cited Findings
- **Ideogram V4 API**: $0.03 (Turbo), $0.06 (Default), $0.10 (Quality). It has about 90% text-rendering accuracy, compared with about 30% for Midjourney on short phrases. Ideogram v3 on fal at $0.03 is recommended for thumbnails with text. — [kie.ai](https://kie.ai/blog/ideogram-v4-pricing), [nodetool](https://nodetool.ai/blog/ai-image-generation-cost) (search snippets)
- **GPT Image 2**: about $0.005–0.006 at low quality, up to $0.211 for high-quality 1024×1024. — [cometapi](https://www.cometapi.com/ai-image-api-pricing/), [invideo Aug 2026](https://invideo.io/blog/ai-image-model-pricing/)
- **FLUX.2**: priced per megapixel, from about $0.014–0.015 (klein tier). — [cometapi](https://www.cometapi.com/ai-image-api-pricing/)
- **Recraft v4.1**: about $0.035, recommended for typography. — [nodetool](https://nodetool.ai/blog/ai-image-generation-cost)
- **satori** (HTML/CSS to SVG, about 14k stars), **Carbon** (about 36k stars) and **ray.so** (about 2.4k stars) are OSS code and card image generators. — [satori](https://github.com/vercel/satori), [carbon](https://github.com/carbon-app/carbon), [ray-so](https://github.com/raycast/ray-so)

### Inferences
- For a vibe-coding blog, code screenshots (ray.so or Carbon) and real app/terminal screenshots are more authentic and anti-slop-friendly than generated images. Reserve Ideogram or GPT Image for YouTube thumbnails and covers.
- Claude Code can generate carousel HTML, which satori or a headless browser then renders to PNG or PDF.

### Gaps
- I did not check Canva API pricing or availability, or Nano Banana (Gemini image) pricing details.
- Russian-market availability and payment constraints for these APIs were not researched.
