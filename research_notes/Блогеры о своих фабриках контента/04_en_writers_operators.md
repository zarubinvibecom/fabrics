# English-language writers, indie hackers and operators who publicly document AI content systems / content factories (as of Sept 2026)

Method note: Research used web search snippets plus direct fetches where the proxy allowed them. Substack (including custom domains such as letters.thedankoe.com), every.to, news.ycombinator.com and timstodz.com were **blocked by the egress proxy**. Many details below therefore come from search-result snippets of the primary pages, not full reads, and are marked that way. GitHub pages could be fetched and are verified. Almost all numbers are **self-reported** by the creator or come from a secondary profile/aggregator unless marked "verified".

## Q1. Which operators run AI-assisted content systems at scale and share the internals?

### Takeaway
The most detailed public build logs in 2025–2026 come from mid-size "AI operator" writers, not the old-guard creator stars. Charlie Hills (open-sourced 17 Claude Code skills, ~3.7k GitHub stars) and Doneyli De Jesus (a 15-agent Claude Code system for his wife's business) share the most internals. The big names (Justin Welsh, Dan Koe, Dan Shipper/Every, Ruben Hassid) mostly sell or productise their system (Eden, Spiral, EasyGen, courses) and do not publish their own pipelines. I found no public content-factory build log from Pieter Levels, McKay Wrigley or Lenny Rachitsky.

### Cited Findings

**Case 1: Charlie Hills (UK marketer; X @charliejhills, Substack charliehills.substack.com "MarTech AI")**
- Audience (self-reported, secondary write-up): about 350,000 followers across LinkedIn, Instagram, Substack, X and YouTube, and "roughly 100 million views a year". He open-sourced his whole content system as 17 Claude Code skills under the MIT licence. — [r2clickthrough write-up](https://www.r2clickthrough.com/inside-charlie-hillss-open-source-social-media-skills/); [Substack post "The 17 Claude skills behind 350k followers"](https://charliehills.substack.com/p/the-simple-350k-follower-ai-content)
- His own framing (X/Substack note): "My entire Claude skills library is now free. 17 skills you can clone in 60 seconds. This is the exact system running my content across LinkedIn, Instagram, Substack, X and YouTube. I test every skill on my own accounts before it ships." — [X post](https://x.com/charliejhills/status/2048428282174156996); [Substack note](https://substack.com/@charliehills/note/c-248482255)
- Repo (verified by fetch, Sept 2026): github.com/charlie947/social-media-skills has about 3,700 stars, 857 forks and 18 commits, under the MIT licence.
  - Skills:
    - Voice: voice-builder, newsletter-voice
    - LinkedIn: profile-optimizer, post-writer, graphic-designer, post-formatter, hook-generator, post-scorer, content-matrix, niche-research, gemini-infographic, gemini-carousel, quote-post
    - Other platforms: reels-scripting, youtube-thumbnail, pinned-comment, analytics-dashboard
  - Architecture: voice-builder creates about-me.md and voice.md, which "every skill below" reads first.
  - Guardrails: "Saving a draft does not publish it". Credentials stay in the user's own environment. Rendered graphics must be inspected at full size and at feed size before they count as reviewed.
  - Source: [GitHub charlie947/social-media-skills](https://github.com/charlie947/social-media-skills)
- The skills are also used as a lead magnet. One X post says: "17 skills turn Claude into your whole social team… Want my setup guide too? → Comment 'SOC…'" — [X post](https://x.com/charliejhills/status/2093705609703309733)
- He also publishes a Claude Code tutorial, "Give me 10 minutes. I'll teach you 80% of Claude Code." — [Substack](https://charliehills.substack.com/p/give-me-10-minutes-ill-teach-you)
- A third-party fork also exists. — [hdaguerre/charlie-hills_social-media-skills](https://github.com/hdaguerre/charlie-hills_social-media-skills)

**Case 2: Doneyli De Jesus (Substack "Signal over Noise"; Principal AI Architect at ClickHouse)**
- Post "How I Automated My Wife's Content Marketing with AI Agents on Claude Code" (from snippets; the full text was blocked):
  - Context: his wife left her corporate job to become a solopreneur and had no time for marketing, so he built her "a 15-agent autonomous system on Claude Code".
  - Scale: about 3,000 files, 24 custom skills (another snippet says 23 skills and 6 autonomous agents), 4 in-conversation subagents, and "a two-wave batch pipeline that handles everything from signal discovery to analytics collection".
  - Output: 10–12 pieces per week across four platforms.
  - The system "knows her voice, follows her standards".
  - Source: [Substack](https://doneyli.substack.com/p/how-i-automated-my-wifes-content)
- Voice enforcement: he built a linter that runs as a Claude Code **PreToolUse hook**. It scans drafts for voice violations and blocks the file write if it finds any. — [Substack, "Quality Gates"/related posts via search snippet](https://doneyli.substack.com/p/quality-gates-for-ai-generated-code)
- "The 3-Layer Claude Code Configuration That Runs 10 Projects": global CLAUDE.md, then project CLAUDE.md, then agent definitions. It is packaged as a template, and the 10 projects include "a content system". — [Substack](https://doneyli.substack.com/p/the-3-layer-claude-code-configuration)
- Related posts: "I Built an AI Chief of Staff That Runs My Life While I Sleep" and "Self healing Claude". — [Substack](https://doneyli.substack.com/p/i-built-an-ai-chief-of-staff-that)
- GitHub (verified by fetch): claude-code-langfuse-template (about 107 stars) for "Self-hosted Langfuse for Claude Code session observability". The profile notes 16K Substack views in 6 days for the observability post (self-reported). I did not find a public repo of the content system itself. — [GitHub doneyli](https://github.com/doneyli)

**Case 3: GenAI Unplugged (Substack)**
- "Claude Code Content System: Full AI System Pipeline From Research to Publish" describes 4 slash commands: /research, /draft, /review and /repurpose. /repurpose writes LinkedIn posts, X threads and Substack Notes. Claimed cost is about **$1.50 per article** (self-reported). Setup is about 15 minutes: drop in a folder, set API keys and edit one brand-voice file. The post includes real test-run outputs and a drop-in scaffold. — [Substack](https://genaiunplugged.substack.com/p/claude-code-content-system-full-ai-pipeline)
- Companion posts cover a 3-agent parallel research team and 5 research subagents. — [Substack](https://genaiunplugged.substack.com/p/claude-code-agents-ai-research-team)

**Case 4: Alex Finn (X @AlexFinn)**
- Profile (secondary source, self-reported): about 320k X followers and 55k YouTube subscribers. He owns Creator Buddy (about $300k ARR). — [search snippet / Grokipedia](https://grokipedia.com/page/Alex_Finn)
- On Peter Yang's podcast he demonstrated a Claude Code "Claude Life" system: slash commands and sub-agents for AI-news curation, brain-dump analysis and a **newsletter research agent** that "saves hours weekly". — [Peter Yang podcast episode](https://creators.spotify.com/pod/profile/peter-yang42/episodes/Full-Tutorial-Build-an-AI-Co-Pilot-for-Your-Life-with-Claude-Code--Alex-Finn-e37hem7)
- Mode: tutorial and selling (Skool community, Creator Buddy). This is not a full build log of his own posting pipeline. — [Skool](https://www.skool.com/@alex-finn-9189)

**Case 5: Ruben Hassid (LinkedIn; Substack ruben.substack.com; founder of EasyGen)**
- Follower counts vary by source: 500K+ (older) and about 798K (more recent secondary). He brands himself as the creator who "taught LinkedIn that you could write with AI and say so out loud". — [magicpost profile](https://magicpost.in/blog/who-is-ruben-hassid); [viralbrain](https://www.viralbrain.ai/heroes/ruben-hassid-shpn4v7r)
- Claim: "Most people will never hit 10,000 Linkedin followers. But I did it (again) in 17 days (using AI)", with a linked Substack guide. — [Substack note](https://substack.com/@ruben/note/c-227596115)
- Synthesia case study (vendor-published): he used an AI avatar/"digital twin" with voice cloning and reached "60M+ video views" in a few months. — [Synthesia](https://www.synthesia.io/case-studies/ruben-hassid)
- Mode: open about using AI, but the system is sold through EasyGen and paid guides. I found no code or repo.

**Case 6: Dan Koe (letters.thedankoe.com; X)**
- In May 2026 he launched **Eden**, a research and writing app. You search "millions of high-performing posts" across X, YouTube, Instagram, TikTok, LinkedIn and Substack, sort them by views or an "outlier multiplier", save the winners, and rewrite them "in a voice you've trained on your own content". — [Eden review](https://hypertools.so/tool/eden); [Dan Koe, "I built the writing app I've always wanted"](https://letters.thedankoe.com/p/i-built-the-writing-app-ive-always)
- Audience figure: "179K followers" per a third-party playbook. This figure is uncertain; other sources give much larger X numbers. — [captureflow](https://captureflow.ai/playbooks/dan-koe)
- Mode: productised (Eden), plus viral prompt essays such as "This prompt will change your life". — [letters.thedankoe.com](https://letters.thedankoe.com/p/this-prompt-will-change-your-life)

**Case 7: Every.to / Dan Shipper**
- Every builds Spiral, an "AI ghostwriter with taste". Spiral 4.0 "goes agent-native" and is available through MCP, CLI and API. A Claude Code cleanup command calls Spiral to generate tweets about new features. — [Every, "Spiral 4.0 Goes Agent-native"](https://every.to/on-every/spiral-4-0-goes-agent-native) (snippet only); [podcast "Spiral: Designing an AI Ghostwriter With Taste"](https://podscan.fm/podcasts/ai-and-i/episodes/spiral-designing-an-ai-ghostwriter-with-taste-1)
- The compound-engineering Claude Code plugin (Shipper and Kieran Klaassen) is a coding workflow, not a content workflow, but Every's culture of shipping content with agents grows out of it. — [Dan Shipper on X](https://x.com/danshipper/status/1957469842178441523)

**Case 8: Justin Welsh**
- His well-known system is manual repurposing: the "Content Matrix" and the "5-12-3 rule" (each piece works in 5 seconds, stays relevant for 12 months and lives on at least 3 platforms). — [justinwelsh.me](https://www.justinwelsh.me/article/content-matrix); [TweetHunter summary](https://tweethunter.io/blog/justin-welsh-content-repurposing-system)
- July 2026 essay "Having fun is the new moat" (from a search snippet): "AI can now replicate content, systems, and funnels in an afternoon". He positions himself on what AI can't copy. — [justinwelsh.me essays](https://www.justinwelsh.me/article/content-matrix) (snippet; exact URL not confirmed)

**Case 9: Pieter Levels (@levelsio)**
- He publicly documents coding with Claude Code on a VPS (a June 2026 thread about "almost a year" of doing this). He builds apps by phone, for example infiniteslop.ai. I found **no evidence** of an AI content factory for his own posting. — [levels.io/2026](https://levels.io/2026); [X](https://x.com/levelsio/status/2103947526160179485); [explainx summary](https://explainx.ai/blog/claude-code-vps-production-workflow-levelsio-june-2026)

**Other open-source LinkedIn/content skill repos (smaller authors)**
- [sergebulaev/linkedin-skills](https://github.com/sergebulaev/linkedin-skills): 11–12 Claude Code and Codex skills (post writer with "20 proven 2026 hook formulas", post audit against algorithm rules and AI-tell patterns). Nothing publishes without approval: the skills "wait for your approval before anything gets published".
- [marian-kamenistak/linkedin-post-writing-skill](https://github.com/marian-kamenistak/linkedin-post-writing-skill): 4-file Claude Projects system with voice calibration, "anti-AI detection" and a weekly workflow.
- [alokesharma/geo-content-engine](https://github.com/alokesharma/geo-content-engine): research-grounded pipeline with a "run-halting anti-AI-writing gate".
- [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills): marketing skills for Claude Code (copywriting, SEO, CRO).

### Inferences
- Publishing internals, especially as MIT-licensed skills, now works as a growth and lead-gen tactic in itself ("comment X for the guide"). Transparency and selling overlap: Hills, Finn and Hassid all monetise around the system.
- The most detailed engineering logs (Doneyli, GenAI Unplugged) come from engineers with smaller audiences, not from mega-creators.
- No big creator (Welsh, Koe, Shipper, Levels) publishes metrics that link their follower growth to an AI pipeline. Hassid's "10k in 17 days using AI" is the closest, and it is self-reported.

### Gaps
- I could not find public build logs from McKay Wrigley or Lenny Rachitsky about content systems. McKay's public output is coding and agents tutorials, which were not verified here.
- I could not read the full text of the Doneyli, Ruben, Dan Koe or Every posts (proxy block), so exact dates, cost per month and stack details (data store, scheduler) are missing.
- I found no independently verified follower or impression growth for any case.

## Q2. What recurring design decisions do they describe?

### Takeaway
The dominant pattern has five parts: a single persistent **voice file** that every skill reads; **modular skills or slash commands per stage** (research, draft, score or review, repurpose, design, analytics); **explicit human approval** before anything publishes; **automated anti-AI-tell gates**; and one-to-many **repurposing** across 3–5 platforms, with analytics fed back in.

### Cited Findings
- **Voice file as foundation:**
  - Hills: voice-builder emits voice.md and about-me.md, which all skills read first. — [GitHub](https://github.com/charlie947/social-media-skills)
  - GenAI Unplugged: "edit one brand-voice file". — [Substack](https://genaiunplugged.substack.com/p/claude-code-content-system-full-ai-pipeline)
  - Dan Koe's Eden: a voice "trained on your own content". — [hypertools](https://hypertools.so/tool/eden)
- **Stage decomposition:**
  - GenAI Unplugged: /research, /draft, /review, /repurpose. — [Substack](https://genaiunplugged.substack.com/p/claude-code-content-system-full-ai-pipeline)
  - Doneyli: a two-wave batch pipeline from "signal discovery to analytics collection". — [Substack](https://doneyli.substack.com/p/how-i-automated-my-wifes-content)
  - Hills: hook-generator, then post-writer, then post-scorer, then formatter/graphics. — [GitHub](https://github.com/charlie947/social-media-skills)
- **Human-in-the-loop:**
  - Hills: "Saving a draft does not publish it". — [GitHub](https://github.com/charlie947/social-media-skills)
  - sergebulaev skills wait for approval before publishing. — [GitHub](https://github.com/sergebulaev/linkedin-skills)
- **Hard quality gates:**
  - Doneyli: a PreToolUse hook that blocks writes on voice violations. — [Substack](https://doneyli.substack.com/p/quality-gates-for-ai-generated-code)
  - geo-content-engine: a run-halting anti-AI-writing gate. — [GitHub](https://github.com/alokesharma/geo-content-engine)
  - Post Audit against AI-detection patterns. — [GitHub](https://github.com/sergebulaev/linkedin-skills)
- **Repurposing ratios:**
  - Welsh's 5-12-3 rule (at least 3 platforms per piece). — [TweetHunter](https://tweethunter.io/blog/justin-welsh-content-repurposing-system)
  - Doneyli: 10–12 pieces per week across 4 platforms. — [Substack](https://doneyli.substack.com/p/how-i-automated-my-wifes-content)
  - Hills: 5 platforms from one system. — [X](https://x.com/charliejhills/status/2048428282174156996)
- **Analytics and outlier loops:**
  - Hills: analytics-dashboard skill. — [GitHub](https://github.com/charlie947/social-media-skills)
  - Eden: sort by "outlier multiplier" to find ideas to rewrite. — [hypertools](https://hypertools.so/tool/eden)
  - Doneyli: analytics collection stage. — [Substack](https://doneyli.substack.com/p/how-i-automated-my-wifes-content)
- **Observability:** Doneyli self-hosts Langfuse for Claude Code session tracing. — [GitHub](https://github.com/doneyli)
- **Cost:** about $1.50 per article (GenAI Unplugged, self-reported). — [Substack](https://genaiunplugged.substack.com/p/claude-code-content-system-full-ai-pipeline)
- **Config layering:** global CLAUDE.md, then project CLAUDE.md, then agent definitions (Doneyli). — [Substack](https://doneyli.substack.com/p/the-3-layer-claude-code-configuration)

### Inferences
- Builders independently arrived at "sounds human" gates (anti-AI-tell linters and scorers). This implies they all hit the same failure mode: generic AI voice hurts reach (see Q3).
- Claude Code (CLI, skills, hooks, subagents) has become the default runtime for these indie systems in 2026. Earlier systems tended to use Zapier, Make or n8n with ChatGPT; this is an inference from source mix, not measured.

### Gaps
- Few sources say what data store they use (most are file- or markdown-based repos; Doneyli has about 3,000 files). None described a database or a scheduler in detail in the parts I could access.
- I found no reported monthly running costs except the GenAI Unplugged per-article figure.

## Q3. Negative experiences / reversals

### Takeaway
I found no well-documented first-person story from a named top creator of "I reverted to manual writing" in the sources I could access. The negative evidence is:
- platform-level (LinkedIn's 2026 "AI slop" crackdown and reported reach penalties for AI-sounding posts);
- community backlash (the Hacker News reaction to OneUptime's 12k-post AI SEO dump, and HN rules against AI comments);
- quiet repositioning by big creators toward "human/fun as moat".

### Cited Findings
- LinkedIn crackdown (third-party analyses, mid-2026):
  - Forbes, "What LinkedIn's AI Slop Crackdown Means For Your Posts" (Aug 10, 2026). — [Forbes](https://www.forbes.com/sites/jodiecook/2026/08/10/what-linkedins-ai-slop-crackdown-means-for-your-posts/)
  - Forbes, "5 LinkedIn Content Moves LinkedIn Started Punishing In 2026" (Jul 23, 2026). — [Forbes](https://www.forbes.com/sites/jodiecook/2026/07/23/5-linkedin-content-moves-linkedin-started-punishing-in-2026/)
  - Entrepreneur on LinkedIn pushing back on AI slop. — [Entrepreneur](https://www.entrepreneur.com/business-news/tired-of-ai-slop-on-your-linkedin-feed-heres-how-the-company-is-pushing-back)
- Reach numbers (vendor or agency claims, not verified; treat with caution):
  - "posts that read as AI get 21% less engagement than the same author's human-sounding posts" (from a 134k-post study). — [Ligo Social, State of LinkedIn 2026](https://ligosocial.com/research/state-of-linkedin-2026)
  - Purely AI posts show about 30% less reach and 55% less engagement. — [orbitrevolution](https://www.orbitrevolution.tech/blog/the-great-linkedin-cleanup-why-your-ai-posts-are-dying) / [yepads](https://yepads.com/linkedin-algorithm-changes-2026-why-linkedin-reach-is-dropping/)
- OneUptime:
  - On April 4, 2026 it pushed 12,000 AI-written blog posts to its public repo in a single commit (a long-tail SEO flood). It drew HN criticism and was flagged as a potential "scaled content abuse" risk under Google's spam policy. — [aiproductivity.ai](https://aiproductivity.ai/news/oneuptime-12000-ai-generated-blog-posts-commit/); [HN thread](https://news.ycombinator.com/item?id=47640722)
  - A related GitHub PR in another repo, "Rewrite AI-generated blog posts to remove AI writing tells", shows a clean-up reversal in practice. — [thinktanktom/site PR #6](https://github.com/thinktanktom/site/pull/6)
- HN sentiment:
  - "It's insulting to read AI-generated blog posts" thread. — [HN](https://news.ycombinator.com/item?id=45722069)
  - "One Month Without AI" thread (2026). — [HN](https://news.ycombinator.com/item?id=49855018)
  - Reports that HN banned AI-generated or AI-edited comments. — [Cybernews](https://cybernews.com/ai-news/hacker-news-bans-ai-generated-and-edited-comments/)
- Partial reversal story: DEV Community post "I Automated My Entire Blog with AI. It Was a Disaster (At First)." Not read in full. — [dev.to](https://dev.to/iyop666/i-automated-my-entire-blog-with-ai-it-was-a-disaster-at-first-2i3a)
- Creator repositioning: Justin Welsh (July 2026) says AI can replicate "content, systems, and funnels in an afternoon" and argues for what AI can't copy. — [justinwelsh.me](https://www.justinwelsh.me/article/content-matrix) (snippet)

### Inferences
- The widespread anti-AI-tell gates in Q2 are an implicit acknowledgement of the reach penalty. Builders do not abandon automation; they add human-voice filters and approval steps.
- Public reversals by big-name creators appear rare or unpublicised. Negative signals come more from platforms and communities than from creator confessions.

### Gaps
- I could not locate (or could not fetch) specific first-person posts from named creators with large audiences saying "I stopped using AI and reach recovered". The HN "One Month Without AI" and dev.to posts were not read in full because of proxy blocks.
- The engagement-penalty percentages come from vendor or agency blogs with unclear methods and have not been independently verified.
