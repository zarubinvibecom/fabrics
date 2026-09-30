# AI Content Factory: End-to-End Architectures and Orchestration (state as of Sept 2026)

Method note: GitHub star counts come live from the GitHub API (retrieved 2026-09-30). Page fetching was blocked by the egress proxy for n8n.io, indiehackers.com, levels.io, substack.com, reddit and most blogs, so many findings below rest on **search-result snippets, not full-page reads**. Treat snippet-derived numbers as "reported by source X", and treat marketing-blog stats with caution (flagged inline).

## 1. Which repos/templates implement full or near-full content factories?

### Takeaway
No single popular open-source repo covers the whole loop (idea → brief → production → approval → publish → analytics → re-ranking) at production quality. The ecosystem splits into (a) **production engines** (short-video generators with 100k+ stars), (b) **HITL agent graphs** (langchain-ai/social-media-agent), (c) **publishing layers** (Postiz, 36k stars, now MCP/agent-native), and (d) new **skill-based agent factories** (Easel, Claude Code skill packs). The only ones that explicitly close the analytics loop are new: Easel (Aug 2026) and custom Claude Code setups described in blog posts.

### Cited Findings
**Near-full pipelines (all 5 stages)**
- **ZJU-REAL/Easel**: 2,550 stars, 393 forks, created 2026-08-28, "discover trends, create content, publish everywhere, and learn what works" across Xiaohongshu, Douyin, Zhihu, Bilibili — [GitHub API](https://github.com/ZJU-REAL/Easel)
  - Five stages: Discover (trend aggregation) → Plan (topics, headlines, scripts) → Create (text, visuals, audio, video) → Publish (per-platform adaptation) → Attribute (performance analysis that updates the account profile) — [README](https://github.com/ZJU-REAL/Easel)
  - Orchestration: one agent on the OpenClaw framework runs the whole workflow and calls 113+ skills backed by Python scripts; `skills/`, `profiles/`, `outputs/` folders. Data model: an **account persona** with 6 dimensions (positioning, style, audience, platforms, preferences, memory) plus **projects** that archive outputs. HITL: a React web workbench with a quality gate before publishing and manual confirmation for sensitive platforms. Stack: FastAPI, FFmpeg, Playwright/Chromium browser automation, Claude/OpenAI-compatible LLMs — [README](https://github.com/ZJU-REAL/Easel)
- **Claude Code "15-agent" system for a real business (Doneyli, Substack)**: 3,000 files, 24 custom skills, 4 in-conversation subagents, and a "two-wave batch pipeline". Loop: *Signal Discovery → Weekly Planning → Two-Wave Production → Review → Publish → Analytics → Loop*. CLAUDE.md works as a "routing table", with three config tiers (global prefs; project settings such as skill triggers, content model, quality gates, platform hierarchy, editorial calendar; persistent memory files) — [doneyli.substack.com](https://doneyli.substack.com/p/how-i-automated-my-wifes-content) (from search snippet; full page blocked)
- **OrangeViolin/content-pipeline**: 220 stars, a Claude Code skill: "One prompt → multi-platform publishing", targets WeChat/Xiaohongshu/podcast — [GitHub](https://github.com/OrangeViolin/content-pipeline)
- **ericosiu/ai-marketing-skills**: 3,592 stars (created Mar 2026), open-source AI marketing skills covering content ops, SEO, growth experiments — [GitHub](https://github.com/ericosiu/ai-marketing-skills)

**HITL agent graph (curation → drafts → approval → scheduling)**
- **langchain-ai/social-media-agent**: 2,817 stars, 510 forks, TypeScript, created Nov 2024, still updated in Sept 2026. "An agent for sourcing, curating, and scheduling social media posts with human-in-the-loop" — [GitHub](https://github.com/langchain-ai/social-media-agent)
  - LangGraph `generate_post` graph: take a URL → check relevance against business context → write a marketing report and draft post → **interrupt into Agent Inbox** for human accept/edit/respond → schedule to X/LinkedIn. Claude does the writing; FireCrawl scrapes; Arcade or native OAuth handles auth; Supabase stores images (5MB max); LangSmith holds traces. A **cron job ingests links from a Slack channel daily** and starts graph runs — [README](https://github.com/langchain-ai/social-media-agent)
  - It has no analytics or feedback stage, and the quickstart mode leaves out GitHub/YouTube parsing, Slack and image selection — [README](https://github.com/langchain-ai/social-media-agent)

**Production engines (video; no approval or analytics)**
- harry0703/**MoneyPrinterTurbo**: 127,400 stars. Topic/keyword → HD short video (LLM script, TTS, subtitles, stock footage, FFmpeg) — [GitHub](https://github.com/harry0703/MoneyPrinterTurbo)
- FujiwaraChoki/**MoneyPrinterV2**: 32,025 stars ("Automate the process of making money online": Twitter bot, YouTube Shorts, outreach); MoneyPrinter v1: 14,017 stars — [GitHub](https://github.com/FujiwaraChoki/MoneyPrinterV2)
- ddean2009/**MoneyPrinterPlus**: 7,155 stars. Batch generation plus auto-publish to Douyin, Kuaishou, Xiaohongshu, Channels — [GitHub](https://github.com/ddean2009/MoneyPrinterPlus)
- RayVentura/**ShortGPT**: 8,000 stars, "Experimental AI framework for youtube shorts / tiktok channel automation" — [GitHub](https://github.com/RayVentura/ShortGPT)
- gemini-youtube-automation: 352 stars, "fully autonomous" Gemini → video → YouTube upload — [GitHub](https://github.com/ChaitanyaEswarRajeshJakki/gemini-youtube-automation)

**Publishing/distribution layer**
- gitroomhq/**postiz-app**: 36,541 stars, 7,042 forks, "The ultimate agentic social media scheduling tool" — [GitHub](https://github.com/gitroomhq/postiz-app). Self-hostable under AGPL-3.0, 30+ networks, public REST API plus webhooks, official `n8n-nodes-postiz` and `@postiz/node` SDK, a hosted MCP server with OAuth that Claude/ChatGPT/Cursor can use, and a CLI plus an installable agent skill — [Postiz blog](https://postiz.com/blog/free-social-media-scheduling-api-n8n-postiz-buffer-blotato-alternative); [openalternative](https://openalternative.co/postiz)

**Idea / research layer**
- ScrapeCreators/**social-media-research-skills**: 2,975 stars (created June 2026). Agent skills for outlier posts, comment mining, competitor teardowns and trends across TikTok/IG/YouTube/Reddit/X/LinkedIn; works with Claude Code, Cursor, Codex — [GitHub](https://github.com/ScrapeCreators/social-media-research-skills)
- apify/apify-mcp-server: 9,112 stars, social-media scraping for agents via MCP — [GitHub](https://github.com/apify/apify-mcp-server)

**n8n templates**
- enescingoz/**awesome-n8n-templates**: 25,670 stars, 280+ free templates including social media and Telegram bots — [GitHub](https://github.com/enescingoz/awesome-n8n-templates)
- n8n.io template #5773 "Generate & schedule social media posts with GPT-4 and Telegram approval workflow" and #6451 "Schedule LinkedIn posts with AI content generation and Telegram approval" — [n8n.io/5773](https://n8n.io/workflows/5773-generate-and-schedule-social-media-posts-with-gpt-4-and-telegram-approval-workflow/); [n8n.io/6451](https://n8n.io/workflows/6451-schedule-linkedin-posts-with-ai-content-generation-and-telegram-approval/) (titles only; page fetch blocked)
- A paid "AI Social Media Content Factory" n8n workflow on Gumroad: idea → composed, illustrated, approved, published posts across X, IG, FB, LinkedIn, Threads, YouTube Shorts, with centralized system prompts and JSON schemas for platform variants; 23 nodes; Telegram bidirectional approval; LLM via OpenRouter — [Gumroad (smartysaini)](https://smartysaini.gumroad.com/l/uewhc) (seller description, via search snippet)
- A "content farming v3" n8n workflow claims 3,000+ blog posts auto-published and **10–30 daily visitors** from cold-start blogs — [Gumroad (0emp0)](https://0emp0.gumroad.com/l/content-farming-v3) (seller claim)

### Inferences
- The star distribution tells you where the value sits: people star **generators** (MoneyPrinterTurbo, 127k) and **publishers** (Postiz, 36k), not orchestrated loops. The "brain" (planning, approval, analytics) is usually custom-built.
- In 2026 the main pattern moved from "n8n graph of LLM nodes" toward **"one agent + a folder of skills + a persona/memory file + MCP tools for publishing"** (Easel, Claude Code setups, Postiz MCP, ScrapeCreators skills). This fits a vibe coder well because the pipeline is markdown and scripts in a git repo.
- For a solo builder, a sensible composition is: research skills (ScrapeCreators/Apify MCP) → Claude Code skills for brief/script/drafts → approval → Postiz (self-hosted or cloud) as the publishing API → metrics pulled back into the store.

### Gaps
- I could not confirm any CrewAI "content crew" repo with meaningful stars. The GitHub search returned only awesome-lists. CrewAI's own examples repo was not checked.
- I found no "n8n content machine" repo with verified stars. Real usage stats (views/imports) for the n8n.io templates were not accessible.
- I did not verify commit cadence beyond `updated_at` (which also counts stars and issues).

## 2. Orchestrator options compared for a solo vibe-coder developer

### Takeaway
There are two workable families. (1) **n8n self-hosted** (flat ~$5–20/mo VPS, visual, native "Send and Wait" Telegram approval, huge template library). (2) **Claude Code / Agent SDK with skills + Routines** (pipeline as code/markdown in git, scheduled cloud runs, MCP to Postiz/Notion). LangGraph gives the best formal HITL and state but costs more engineering. Make/Zapier get expensive per-operation for LLM-heavy multi-step flows. I found little evidence that durable-execution engines (Temporal/Prefect/Dagster) are used for content factories; they are overkill for one person.

### Cited Findings
- **Pricing models**: Make bills per operation (each module run); n8n cloud bills per workflow execution; a 5-step workflow = 5 Zapier tasks but 1 n8n execution — [digidop](https://www.digidop.com/blog/n8n-vs-make-vs-zapier); [F³ Fund It](https://f3fundit.com/workflow-automation-n8n-zapier-make-activepieces-2026/)
- n8n Cloud from ~$20–22/mo for 2,500 executions. Make: free 1,000 ops, $9/mo 10k ops, $29/mo 40k ops. Zapier from $19.99/mo for 750 tasks. Activepieces Community is free self-hosted, Cloud from $15/mo for 10k tasks. Self-hosted n8n costs about $5–20/mo in server fees with unlimited executions — [F³ Fund It](https://f3fundit.com/workflow-automation-n8n-zapier-make-activepieces-2026/); [digitalapplied](https://www.digitalapplied.com/blog/zapier-vs-make-vs-n8n-2026-automation-comparison) (sources differ slightly on figures: $20 vs $22)
- One solo-founder guide recommends Make ($12/mo Core, $21/mo Pro) as "the best balance" for non-coders — [ShippedSolo](https://shippedsolo.com/blog/zapier-vs-make-vs-n8n/) (note: its Make prices differ from the other source's $9/$29, so they are unverified)
- **n8n HITL**: "Send and Wait for Response" is an operation on the Slack, Telegram, Gmail, Discord, MS Teams and WhatsApp nodes. It pauses execution until someone answers, with Approve/Deny inline buttons in Telegram and optional free-text replies — [n8n docs: HITL for tools](https://docs.n8n.io/build/integrate-ai/ai-examples/human-in-the-loop-for-tools); [ryanandmattdatascience](https://ryanandmattdatascience.com/n8n-human-in-the-loop/). There is a community-reported issue ("No action required") when this is used with Agent tools in Telegram — [n8n community](https://community.n8n.io/t/human-in-the-loop-with-agent-tools-telegram-no-action-required-issue-when-using-send-and-wait-for-response/79769)
- **Claude Code Routines** (launched April 2026): a saved prompt + repo(s) + connectors that runs on Anthropic-managed cloud. Triggers: scheduled (hourly/nightly/weekly), API (HTTP POST) and GitHub webhook. Limits are 5 routines/day on Pro, 15 on Max, 25 on Team/Enterprise. Set up at claude.ai/code/routines or with `/schedule` in the CLI — [Better Stack](https://betterstack.com/community/guides/ai/claude-code-routines/); [The Prompt Shelf](https://thepromptshelf.dev/blog/claude-code-routines-scheduled-tasks-guide-2026/) (the daily-run limits come from third-party guides; verify against official docs)
- Claude Code skill-chain pattern: extraction → LinkedIn formatting → X thread → newsletter, each skill with its own input schema and output structure. MCP connects Notion (staging), Blotato/Buffer (scheduling) and the email platform (newsletter drafts). Realistic output: "five LinkedIn drafts, two thread options, and a newsletter section, and you spend 10 minutes picking and lightly editing instead of two hours" — [MindStudio](https://www.mindstudio.ai/blog/content-repurposing-engine-claude-code) (vendor blog)
- A practitioner runs six Claude Code skills (blog, LinkedIn, cold email, Upwork, community, YouTube), each taking an idea "to a finished draft sitting in a CMS, in the user's voice" — [Dominik Gronkiewicz](https://dominikgronkiewicz.com/blog/claude-code-skills-content-pipeline/) (snippet)
- "How We Automate Marketing for 7 Projects on $40/Month — Claude + Codex" — [apsquared](https://apsquared.co/posts/marketing-automation-claude-codex) (title only; page blocked)
- **Agent framework comparison**: LangGraph has "the strongest persistence and checkpointing story" and a first-class `interrupt()` primitive. CrewAI suits fast multi-agent prototyping (HITL through custom tools). The OpenAI Agents SDK leads on simplicity, with approval callbacks in the harness and handoffs that "get awkward for true parallel collaboration". The Claude Agent SDK "leads on lifecycle control", does HITL through event-stream interrupts, and ships built-in file/bash/web/grep tools — [qubittool](https://qubittool.com/blog/ai-agent-framework-comparison-2026); [requesty](https://www.requesty.ai/blog/best-ai-agent-sdks-compared-2026-langchain-crewai-openai-anthropic-google)

### Inferences
- **For a vibe-coder solo dev**, a pragmatic ranking:
  1. **Claude Code + skills + subagents + Routines (+ MCP: Postiz, Notion/Supabase, Telegram)**. The pipeline is plain markdown/code in git, the agent can extend itself, it needs no server, and the cost is folded into the Claude subscription. Downsides: routine-per-day caps, non-deterministic runs, weak native long-running "wait for approval" state (approval has to be modelled as a status in the DB, with the next scheduled run picking it up).
  2. **n8n self-hosted**. Deterministic, visual, best native Telegram approval, cheap. Downsides: JSON workflows are awkward to version and vibe-code, and complex LLM logic gets messy in nodes.
  3. **Hybrid (common in practice)**: n8n for triggers, webhooks, approval buttons and publishing; Claude Code/Agent SDK (called via API or Routine API trigger) for the "creative" steps.
  4. **LangGraph** only if you want formal state machines and interrupts in code (the langchain social-media-agent is a ready template).
- Make/Zapier: fine for prototypes. Per-operation billing punishes multi-step LLM flows. Activepieces is an MIT-ish open alternative to n8n but with a smaller template ecosystem (inference; not deeply verified).
- Temporal/Prefect/Dagster/Windmill: durable execution is useful for heavy video rendering queues, but no content-factory case studies surfaced (see Gaps).

### Gaps
- I found no sourced case studies of Temporal, Prefect, Dagster, Windmill or Mastra used for content pipelines, so no firm pros/cons are cited for them.
- I did not verify the official Anthropic docs for Routine limits and pricing (the figures above come from third-party guides).

## 3. Content state machine / data model and where to store it

### Takeaway
Working systems track each content item through explicit statuses, keep a **persona/voice + memory** artifact separate from items, and keep **per-platform variants** as child records. Storage choice follows the orchestrator: Notion/Airtable for n8n-style no-code setups with a human UI, Supabase/Postgres when scripts and agents write heavily, and a **git repo of markdown with frontmatter** for Claude Code-native factories (the Doneyli system is ~3,000 files).

### Cited Findings
- Easel's data model: account persona (positioning, style, audience, platforms, preferences, memory) + projects archiving outputs with metadata; stages Discover/Plan/Create/Publish/Attribute; the Attribute stage writes back into the profile — [Easel README](https://github.com/ZJU-REAL/Easel)
- langchain social-media-agent state: URL → relevance check → report → post draft → interrupt → scheduled date; images in Supabase storage — [README](https://github.com/langchain-ai/social-media-agent)
- Claude Code factory: a file-based repo (3,000 files); CLAUDE.md holds content model, quality gates, platform hierarchy and editorial calendar; persistent memory files — [Doneyli](https://doneyli.substack.com/p/how-i-automated-my-wifes-content)
- Claude Code repurposing engines use Notion as the staging DB via MCP — [MindStudio](https://www.mindstudio.ai/blog/content-repurposing-engine-claude-code)
- **Storage pricing (2026)**: Airtable Team $20/user/mo (base caps apply, e.g. 125k records/base on Business). Baserow free tier with unlimited DBs and 2GB; Premium $10/user/mo (50k rows); self-hosted has no row limits. NocoDB free tier with 1,000 records; Plus $12/seat with 10k automation runs and 100k API calls/mo; self-host free; 50k+ GitHub stars. Supabase free or $25/project/mo with REST/GraphQL/Realtime. Notion Plus $10/member/mo — [natharia](https://natharia.com/blog/best-no-code-database-platforms-2026); [thefrontkit](https://thefrontkit.com/blogs/airtable-alternatives-2026); [elest.io](https://blog.elest.io/nocodb-vs-baserow-which-open-source-airtable-alternative-should-you-pick/)

### Inferences
- Suggested minimal schema (synthesized from the above, not taken from one source):
  - `ideas` (source, url, signal_score, predicted_score, status: new/shortlisted/rejected)
  - `briefs` (idea_id, angle, audience, hook options)
  - `pieces` (brief_id, script/longform, assets[])
  - `variants` (piece_id, platform, text, media, status: draft → needs_review → approved/rejected(reason) → scheduled → published → failed, scheduled_at, external_post_id)
  - `metrics` (variant_id, t+1h/24h/7d snapshots: impressions, engagement, CTR, followers delta)
  - `persona/voice` doc plus a `learnings` log
- For a Claude Code-centric factory: markdown + YAML frontmatter in git is the most agent-friendly (diffable, no API), with Supabase/SQLite added only for metrics time-series. For a phone-based approval UI, Notion or NocoDB is easier than raw Postgres.
- Rejection reasons are valuable training data for the prompt and voice guide, so store them.

### Gaps
- There is no public canonical schema from a mature open-source factory. The schema above is inferred.

## 4. Human-in-the-loop patterns and quality gates

### Takeaway
The dominant HITL pattern is **approve-before-publish on mobile**: Telegram/Slack buttons in n8n, Agent Inbox in LangGraph, or a status column in Notion or a web workbench. Mature systems add automated quality gates (voice/style checks, platform rules) before the human sees drafts, plus mandatory manual confirmation on risky platforms.

### Cited Findings
- Telegram Approve/Deny inline buttons pause the n8n execution until a tap; the same works on Slack, Discord, WhatsApp, Gmail and Teams — [ryanandmattdatascience](https://ryanandmattdatascience.com/n8n-telegram/); [n8n docs](https://docs.n8n.io/build/integrate-ai/ai-examples/human-in-the-loop-for-tools)
- LangGraph Agent Inbox: human views interrupted runs and accepts/edits/responds — [social-media-agent README](https://github.com/langchain-ai/social-media-agent)
- Easel: a quality gate before publish, manual confirmation for sensitive platforms (Xiaohongshu), review dashboards — [Easel](https://github.com/ZJU-REAL/Easel)
- Claude Code factory: "Review" is an explicit stage and quality gates are defined in CLAUDE.md — [Doneyli](https://doneyli.substack.com/p/how-i-automated-my-wifes-content)
- Picking and editing takes about 10 min instead of 2 h of writing — [MindStudio](https://www.mindstudio.ai/blog/content-repurposing-engine-claude-code)
- Evidence that human editing matters (see Q6): on Reddit, the same content got 127 views/3 upvotes when "polished" versus 1,400 views/89 upvotes when written casually — [Medium (linghonsly)](https://medium.com/@linghonsly/i-got-shadowbanned-on-reddit-heres-what-i-learned-about-the-2025-algorithm-68cb85f445ab) (single anecdote)

### Inferences
- Recommended gates: (1) idea gate (human shortlists weekly from a ranked list); (2) automated lint (banned-phrase list of "AI tells", length and platform rules, fact/link check, LLM-as-judge against the voice guide); (3) final human approve/edit per variant on phone; (4) never auto-post on Reddit or in community venues.
- n8n "Send and Wait" gives the smoothest one-tap mobile approval. In a Claude Code-only setup, the equivalent is a Telegram bot or Notion status that a Routine polls on its next run.

### Gaps
- No quantitative data on approval rates or edit ratios from real factories.

## 5. Analytics feedback loop: ranking future ideas from performance

### Takeaway
Only a few systems implement it (Easel's "Attribute" stage updates the persona; the Doneyli pipeline has Analytics → Loop). The practical mechanism is: collect metrics at fixed intervals → store per variant → periodically have an LLM summarize "what worked" into a learnings/memory file → feed it into idea scoring. Research suggests using **pairwise comparisons** rather than absolute LLM scores for ranking.

### Cited Findings
- Easel's Attribute stage analyzes performance and updates the account profile — [Easel](https://github.com/ZJU-REAL/Easel)
- Doneyli loop: "…Publish → Analytics → Loop" — [Doneyli](https://doneyli.substack.com/p/how-i-automated-my-wifes-content)
- LLMs are poorly calibrated when asked for absolute scores but reach non-trivial accuracy on **pairwise** "which idea is better" judgments (Claude-3.5-Sonnet 71.4% in the idea-ranking study) — [arXiv 2409.04109](https://arxiv.org/pdf/2409.04109)
- Closed-loop agent design: downstream agents emit structured quality signals into cross-session memory, which accumulates what worked without retraining — [arXiv 2603.18073](https://arxiv.org/pdf/2603.18073) (snippet summary)
- Outlier-post detection skills (ScrapeCreators) help rank ideas by external performance signals — [GitHub](https://github.com/ScrapeCreators/social-media-research-skills)

### Inferences
- Simple solo implementation: a weekly Routine pulls platform metrics (via Postiz analytics or platform APIs) → normalizes them by account baseline (for example, engagement vs. trailing median) → tags each post with features (topic, format, hook type, length) → asks the LLM to update `learnings.md` → the idea-ranking step does pairwise tournaments of new ideas, conditioned on learnings plus external outlier signals.
- Keep a small exploration budget (for example 20% of slots for untested topics) so the loop does not collapse onto one format. This is standard bandit practice, not from a cited source.

### Gaps
- No public numbers showing that a feedback loop measurably improved performance in a solo content factory.

## 6. Case studies: results, costs, failures

### Takeaway
Reported wins are mostly **time savings** (roughly 80% less time) and volume increases. Reported failures are consistent: platforms suppress generic AI content (LinkedIn 2026 changes, Reddit shadowbans, Google's scaled-content-abuse actions), and distribution automation often produces no business results. The winning pattern is AI drafting + human editing at modest volume, not fully autonomous mass posting.

### Cited Findings
**Positive / time savings**
- An n8n + GPT case study (DEV, via snippet): after 3 months, weekly pieces went from 4–5 to 18–22, content hours from 15 to 3 per week, LinkedIn impressions from about 2,000 to about 12,000 per week, and blog posts from 2 to 8 per month; OpenAI cost about $45/mo — [DEV (techifive)](https://dev.to/techifive/automating-my-entire-content-workflow-using-n8n-gpt-3b5k) (self-reported; single author)
- 7 projects marketed for about $40/mo with Claude + Codex — [apsquared](https://apsquared.co/posts/marketing-automation-claude-codex) (title claim)

**Failures and warnings**
- Indie Hackers "AI runs 70% of my distribution": spent **$400/mo at peak on six AI distribution stacks → zero signups**. After switching, output doubled while cost dropped to **$19/mo**. Lesson: they "had been automating the 70% of distribution work that doesn't convert while ignoring the 30% that does" — [Indie Hackers](https://www.indiehackers.com/post/ai-runs-70-of-my-distribution-the-exact-stack-fda9c0d2c9) (via snippet)
- Pieter Levels (@levelsio): "Indie hackers build fancy AI factories but have no money or traffic" — [levels.io](https://levels.io/indie-hackers-ai-factories-no-money-traffic) (title and snippet; page blocked)
- **LinkedIn**: algorithm changes announced May 20, 2026 target low-quality AI posts, comments and automation tools. Posts flagged by the "AI slop" report button reportedly get about 40% fewer views. The 360Brew model reads post + author profile + reader history — [Neil Patel](https://neilpatel.com/blog/linkedin-ai-slop-crackdown-content-strategy/); [vulse](https://vulse.co/blog/linkedin-ai-slop-button-1-million-reports); [media-all.in](https://media-all.in/en/blog/linkedin-fall-2026-algorithm-changes/). Claims such as "94% detection accuracy" and a "LinkedIn Pulse study: −30% reach, −55% engagement for purely AI posts" appear in aggregator blogs without primary sources, so treat them as unverified — [zoomsphere](https://www.zoomsphere.com/blog/linkedin-algorithm-2026-why-generic-ai-content-kills-your-organic-reach)
- **Reddit**: Reddit reportedly partnered with OpenAI to detect AI content. The "polished vs casual" test gave 127 views/3 upvotes versus 1,400/89. Shadowbans hit repetitive, automated or generic AI comments and shared IPs, and users often don't know for weeks — [Medium](https://medium.com/@linghonsly/i-got-shadowbanned-on-reddit-heres-what-i-learned-about-the-2025-algorithm-68cb85f445ab); [readyt.ai "Reddit Automation Crackdown 2026"](https://www.readyt.ai/blog/reddit-automation-crackdown-2026/); [reddgrow](https://reddgrow.ai/blog/reddit-shadowban-explained/)
- **Google/SEO**: one test site peaked at 2,426 daily impressions (Apr 5, 2026) and collapsed on Apr 9 to 15; a control site died on Jun 26 (859 → 85). Both were deindexed with no notice — [Otterly "2,000 AI blogs" experiment](https://otterly.ai/blog/geo-experiment-2000-ai-blogs-google-penalization/). A site with 22,000 AI pages was wiped from Google — [tailride](https://tailride.so/blog/google-penalty-22000-ai-pages). The March 2026 core update named scaled content abuse; sites with 1,000+ unedited AI articles reportedly saw drops of 40–90%, while 50–100 edited AI articles saw gains of 30–80% — [digitalapplied](https://www.digitalapplied.com/blog/scaled-content-abuse-google-march-update-ai-pages-decimated) (aggregate figures, methodology unclear)
- An AI content-mill company (Brown Brothers Media) halted publishing after a Futurism investigation — [Futurism](https://futurism.com/artificial-intelligence/brown-brothers-media-halts-publishing)
- A cold-start auto-blog seller claims 3,000+ posts give only **10–30 daily visitors** — [Gumroad](https://0emp0.gumroad.com/l/content-farming-v3). This is a weak result even by the seller's own framing.

### Inferences
- For a "vibe coding" content factory, the audience (developers) is especially allergic to slop. The factory should maximize **human signal**: real build logs, screenshots, repo diffs and personal takes, with AI doing research, structuring, repurposing and scheduling.
- Volume is not the bottleneck; distinctiveness is. Keep the approval gate mandatory.

### Gaps
- Direct Reddit threads (r/n8n, r/AI_Agents, r/ClaudeAI) could not be fetched (egress blocked), and search did not surface specific high-quality threads with numbers. HN threads were not retrieved.
- There is no verified primary source for the LinkedIn detection-accuracy and "Pulse study" figures.

## 7. Budget: realistic monthly cost of a full stack

### Takeaway
A lean solo stack runs about **$25–80/mo** in cash (VPS + LLM API + optional scraping) if you self-host n8n, Postiz and NocoDB/Baserow, or use a Claude subscription you already pay for. Adding AI video, voice or image generation plus paid scrapers pushes it to about $100–300+. Case studies show overspending (for example $400/mo) without results is common.

### Cited Findings
- n8n self-hosted about $5–20/mo server, unlimited executions; n8n cloud from about $20–22/mo — [F³ Fund It](https://f3fundit.com/workflow-automation-n8n-zapier-make-activepieces-2026/)
- Make $9–29/mo; Zapier from $19.99/mo (750 tasks); Activepieces Cloud from $15/mo — [F³ Fund It](https://f3fundit.com/workflow-automation-n8n-zapier-make-activepieces-2026/)
- Postiz self-hosted costs nothing beyond your server (AGPL); API and webhooks are on the entry "Standard" cloud plan — [Postiz blog](https://postiz.com/blog/free-social-media-scheduling-api-n8n-postiz-buffer-blotato-alternative)
- DB: Supabase free or $25; NocoDB/Baserow free self-hosted; Notion Plus $10; Airtable Team $20/user — [natharia](https://natharia.com/blog/best-no-code-database-platforms-2026)
- LLM API costs in n8n content flows: about $5–15/mo, $10–30/mo, or about $45/mo depending on volume — [DEV (techifive)](https://dev.to/techifive/automating-my-entire-content-workflow-using-n8n-gpt-3b5k); [scientyficworld](https://scientyficworld.org/linkedin-automation-using-n8n-and-openai/)
- Reported totals: $19/mo after optimization vs $400/mo peak with no result — [Indie Hackers](https://www.indiehackers.com/post/ai-runs-70-of-my-distribution-the-exact-stack-fda9c0d2c9); about $40/mo for 7 projects — [apsquared](https://apsquared.co/posts/marketing-automation-claude-codex)
- Generic ranges quoted: $50–200/mo basic, $500–1,000 intermediate — [Indie Hackers affiliate guide](https://www.indiehackers.com/post/how-to-automate-affiliate-marketing-with-ai-complete-guide-0042f8317f) (generic guidance)
- Claude Code Routines are included in Pro/Max/Team plans, with daily-run caps of 5/15/25 — [Better Stack](https://betterstack.com/community/guides/ai/claude-code-routines/)

### Inferences
- Example budget for a Claude Code-centric solo factory: Claude Pro/Max (already paid for dev work, so marginal about $0), a VPS for Postiz + n8n + NocoDB at about $6–12, Apify/ScrapeCreators credits at about $0–49, optional image/video APIs at about $10–50. Total marginal cost is about **$20–110/mo**.
- The dominant "cost" is human review time (about 10–30 min/day), not tooling.

### Gaps
- No verified current prices for Claude subscription tiers, ScrapeCreators or Apify plans, or video-gen APIs (ElevenLabs, HeyGen etc.) were collected here.
