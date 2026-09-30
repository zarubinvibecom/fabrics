# Automated / AI-assisted video production pipelines for a vibe-coding channel (as of 2026-09-30)

Method note: GitHub star counts, licenses and last-push dates came from the GitHub Search API on 2026-09-30 (a snapshot; stars change daily). The direct GitHub REST API, support.google.com (the official YouTube policy page), hollywoodreporter.com and tech-insider.org were blocked by the network proxy. Policy facts therefore rely on secondary coverage, which is flagged below. No Reddit threads came back in search (site:reddit.com returned no reddit.com URLs), so the "Reddit sentiment" findings are indirect.

## Q1. Open-source repos per pipeline step (stars, license, maturity, GPU needs)

### Takeaway
There is a mature open-source option for every step. Transcription: faster-whisper, WhisperX, whisper.cpp. Silence cutting: auto-editor. Programmatic video: Remotion, Motion Canvas, MoviePy. TTS: F5, Chatterbox, Fish Speech, IndexTTS, VibeVoice, Kokoro. Translation/dubbing: VideoLingo, pyvideotrans. Terminal recording: VHS, asciinema. The "all-in-one faceless shorts" repos (MoneyPrinterTurbo, ShortGPT) are popular but make exactly the templated stock-footage content YouTube now demonetizes. Lip-sync repos (LatentSync, MuseTalk) have gone stale. Check licenses: Remotion, Fish Speech, MuseTalk, IndexTTS and Cap are not plain permissive licenses.

### Cited Findings
Snapshot table (stars / SPDX license / last push), from the GitHub Search API on 2026-09-30:

**Faceless / shorts generators**
- harry0703/MoneyPrinterTurbo: 127,399 stars, MIT, pushed 2026-09-30 (active). It turns one keyword into a short: LLM script, stock footage, TTS and subtitles. — [GitHub](https://github.com/harry0703/MoneyPrinterTurbo)
- FujiwaraChoki/MoneyPrinter (the original, MoviePy-based): 14,017 stars, MIT, last push 2026-03-26. — [GitHub](https://github.com/FujiwaraChoki/MoneyPrinter)
- RayVentura/ShortGPT: 8,000 stars, MIT, last push 2025-02-10. It looks stale, which is roughly 19 months without a push. — [GitHub](https://github.com/RayVentura/ShortGPT)
- elebumm/RedditVideoMakerBot: 12,537 stars, GPL-3.0, active (2026-09-30). — [GitHub](https://github.com/elebumm/RedditVideoMakerBot)

**Long-to-short auto-clippers (OpusClip alternatives)**
- SamurAIGPT / Anil-matcha AI-Youtube-Shorts-Generator. It describes itself as an "open-source alternative to Opus Clip, Vidyo.ai, Klap & SubMagic" with LLM highlight detection, Whisper transcription and auto vertical crop. I did not get a star count. — [GitHub](https://github.com/samuraigpt/ai-youtube-shorts-generator)
- ClipsAI/clipsai: 544 stars, MIT, last push 2024-01-17. It is effectively abandoned. — [GitHub](https://github.com/ClipsAI/clipsai)
- Newer local-first clippers (star counts not collected): GrepCut/OpenClipper (a Tauri desktop app with AI highlights, animated captions and auto-reframe) — [GitHub](https://github.com/GrepCut/OpenClipper); fralapo/clippyme (Gemini viral-moment detection, active-speaker reframing, scheduling to TikTok, Reels and Shorts) — [GitHub](https://github.com/fralapo/clippyme); ColinGPT9/clips-studio (runs locally, speaker-aware face tracking) — [GitHub](https://github.com/ColinGPT9/clips-studio); Shaarav4795/ClippedAI — [GitHub](https://github.com/Shaarav4795/ClippedAI). There is also a topic hub. — [GitHub topic](https://github.com/topics/opus-clip-alternative)

**Auto-editing / cutting**
- WyattBlue/auto-editor: 5,397 stars, Unlicense, active (2026-09-19). It cuts silence and dead space. — [GitHub](https://github.com/WyattBlue/auto-editor)
- mifi/lossless-cut: 44,172 stars, GPL-2.0, active. It is a GUI for lossless trimming. — [GitHub](https://github.com/mifi/lossless-cut)

**Transcription / captions**
- SYSTRAN/faster-whisper: 25,642 stars, MIT, active. — [GitHub](https://github.com/SYSTRAN/faster-whisper)
- m-bain/whisperX (word-level timestamps and diarization, which animated captions need): 24,318 stars, BSD-2-Clause, active. — [GitHub](https://github.com/m-bain/whisperX)
- ggml-org/whisper.cpp (runs on CPU and Apple Silicon): 54,045 stars, MIT, active. — [GitHub](https://github.com/ggml-org/whisper.cpp)

**Programmatic video**
- remotion-dev/remotion: 61,259 stars, custom license ("NOASSERTION"), active. — [GitHub](https://github.com/remotion-dev/remotion). The license is free for individuals, for-profit companies with up to 3 employees, and non-profits. Larger companies need a Company License: $25/seat/month for creators, and automation has a $100/month minimum (prices seen 2026-09-11). — [remotion.pro/license](https://www.remotion.pro/license); [reactvideoeditor.com](https://www.reactvideoeditor.com/blog/is-remotion-free)
- motion-canvas/motion-canvas: 19,210 stars, MIT, last push 2026-07-02. — [GitHub](https://github.com/motion-canvas/motion-canvas)
- Revideo (a Motion Canvas fork that adds headless rendering, audio and a library-first API) has been folded into Midrender, a commercial visual editor. Recent engine changes "have not yet been upstreamed" to the open-source repo, so treat it as semi-maintained. — [Midrender: next chapter of Revideo](https://midrender.com/revideo); [PkgPulse comparison](https://www.pkgpulse.com/guides/remotion-vs-motion-canvas-vs-revideo-programmatic-video-2026)
- Zulko/moviepy: 14,937 stars, MIT, active (2026-08-26). — [GitHub](https://github.com/Zulko/moviepy)

**TTS / voice cloning**
- microsoft/VibeVoice ("Open-Source Frontier Voice AI"; long-form, multi-speaker): 54,554 stars, MIT, active. — [GitHub](https://github.com/microsoft/VibeVoice)
- fishaudio/fish-speech: 32,897 stars, custom license (NOASSERTION; check whether the weights allow commercial use), active. — [GitHub](https://github.com/fishaudio/fish-speech)
- resemble-ai/chatterbox: 26,626 stars, MIT, last push 2026-07-21. — [GitHub](https://github.com/resemble-ai/chatterbox)
- index-tts/index-tts ("industrial-level controllable zero-shot TTS"): 24,236 stars, custom license, active. — [GitHub](https://github.com/index-tts/index-tts)
- SWivid/F5-TTS: 15,316 stars, MIT (code), active. — [GitHub](https://github.com/SWivid/F5-TTS)
- k2-fsa/OmniVoice ("voice cloning TTS for 600+ languages"): 14,079 stars, Apache-2.0, active. — [GitHub](https://github.com/k2-fsa/OmniVoice)
- QwenLM/Qwen3-TTS: 13,596 stars, Apache-2.0, last push 2026-03-17. — [GitHub](https://github.com/QwenLM/Qwen3-TTS)
- hexgrad/kokoro (small, fast, no cloning): 9,090 stars, Apache-2.0, last push 2025-08-06. — [GitHub](https://github.com/hexgrad/kokoro)
- coqui-ai/TTS (XTTS): 46,092 stars, MPL-2.0, last push 2024-08-16. It is stale/unmaintained. — [GitHub](https://github.com/coqui-ai/TTS)

**Lip-sync / avatars**
- bytedance/LatentSync: 6,103 stars, Apache-2.0, last push 2025-06-20 (stale). — [GitHub](https://github.com/bytedance/LatentSync)
- TMElyralab/MuseTalk: 6,651 stars, custom license, last push 2025-09-26 (stale). — [GitHub](https://github.com/TMElyralab/MuseTalk)

**Translation / dubbing**
- Huanshere/VideoLingo (subtitle cutting, translation, alignment and dubbing): 18,550 stars, Apache-2.0, active. — [GitHub](https://github.com/Huanshere/VideoLingo)
- jianchang512/pyvideotrans (translates video and embeds dubbing and subtitles): 19,184 stars, GPL-3.0, active. — [GitHub](https://github.com/jianchang512/pyvideotrans)

**B-roll generation (open weights)**
- Wan-Video/Wan2.2: 17,677 stars, Apache-2.0, active. — [GitHub](https://github.com/Wan-Video/Wan2.2)
- Lightricks/LTX-Video: 10,997 stars, Apache-2.0, last push 2026-01-05. — [GitHub](https://github.com/Lightricks/LTX-Video)

**Screen / terminal recording**
- charmbracelet/vhs (scripted terminal GIF/MP4 from a .tape file): 21,027 stars, MIT, active. — [GitHub](https://github.com/charmbracelet/vhs)
- asciinema/asciinema: 17,852 stars, GPL-3.0, active. — [GitHub](https://github.com/asciinema/asciinema)
- CapSoftware/Cap (open-source Loom / Screen Studio alternative): 22,975 stars, custom license, active. — [GitHub](https://github.com/CapSoftware/Cap)
- siddharthvaddem/openscreen (a free Screen Studio-style demo recorder): 39,956 stars, MIT, but **archived** (last push 2026-06-17). Do not build on it. — [GitHub](https://github.com/siddharthvaddem/openscreen)

**Claude Code-native video tooling (new in 2026)**
- hassancs91/claude-youtube-editor. You "record the talking head, Claude Code does the rest: the cut, the visuals, the voice, the sound effects, the thumbnail, and the YouTube upload". Every screen moment is built as Remotion TSX rather than screen-recorded. A "fake-screencast" skill animates a cursor over screenshots along bezier paths, adds click ripples and ken-burns zooms. — [GitHub](https://github.com/hassancs91/claude-youtube-editor); [LearnWithHasan guide](https://learnwithhasan.com/guide/claude-code-video-editing/)
- wilwaldon/Claude-Code-Video-Toolkit: skills and MCP servers for Remotion, Manim, screen recording, YouTube clipping and FFmpeg post-processing. — [GitHub](https://github.com/wilwaldon/Claude-Code-Video-Toolkit)
- screencli: a Claude Code skill that produces a polished MP4 with a gradient background, auto-zoom to each action, click highlights and cursor trails, without a screen-recorder app. — [screencli blog](https://screencli.sh/blog/record-product-demos-with-claude-code)
- MustaphaSteph/vorec-plugins: a Claude Code plugin for screen recording with AI narration, zoom effects, subtitles and 4K export. — [GitHub](https://github.com/MustaphaSteph/vorec-plugins)

### Inferences
- GPU needs (general knowledge, not measured here). Whisper, auto-editor, FFmpeg, Remotion, MoviePy, Kokoro and VHS run fine on a laptop CPU or Apple Silicon. Voice-cloning TTS (F5, Chatterbox, Fish, IndexTTS, VibeVoice) is practical on a consumer NVIDIA GPU with about 8–16 GB VRAM. Wan2.2 and LTX-Video, and lip-sync like LatentSync, want 12–24 GB+ or rented cloud GPUs. A solo creator without a GPU should use cloud APIs for voice cloning and B-roll.
- For a vibe-coding channel, the highest-leverage open-source pieces are faster-whisper/WhisperX, auto-editor, Remotion (with Claude Code writing the compositions), VHS for reproducible terminal demos, and VideoLingo/pyvideotrans for EN↔RU. Faceless generators like MoneyPrinterTurbo don't fit coding content, and their output is the kind of content targeted by policy (see Q4).
- ComfyUI is the usual host for Wan/LTX/Hunyuan workflows. I did not collect its stats, but it is the de facto open-source node UI for them.

### Gaps
- Star counts were not retrieved for ComfyUI, Revideo, AI-Youtube-Shorts-Generator, CosyVoice, KlicStudio, OpenShorts or the newer clippers.
- Exact VRAM requirements per model were not verified from the READMEs.
- The license terms for Fish Speech, IndexTTS, MuseTalk and Cap (custom/"NOASSERTION") were not read. Check them before commercial use.
- XTTS's CPML non-commercial weight license comes from prior knowledge and is not verified here.

## Q2. SaaS leaders and prices (2026)

### Takeaway
A solo creator's SaaS layer typically costs $10–30 per tool per month. Clipping: OpusClip, Vizard, Submagic. Editing: Descript. Recording: Screen Studio, Cap, Tella. Voice: ElevenLabs. Avatar/dubbing: HeyGen. B-roll is usage-based per second. Kling is cheapest, and Veo 3.1 has the highest quality. **Sora is gone:** the app shut down 2026-04-26 and the API on 2026-09-24.

### Cited Findings
- **OpusClip.** Free: 60 credits/mo, watermark, clips expire after 3 days. Starter: $15/mo for 150 credits. Pro: $29/mo, or $14.50/mo billed annually, for 300 credits. — [overlap.ai / reap.video roundup via search](https://overlap.ai/blogs/opusclip-alternatives)
- **Vizard** (as of 2026-09-17). Creator: $14.50/mo billed yearly ($29 monthly). Business: $19.50/mo yearly ($39 monthly). Both plans include 600 credits/mo, and 1 credit = 1 minute of video. — [overlap.ai](https://overlap.ai/blogs/vizard-alternatives)
- **Submagic** (as of 2026-09-17). Starter: $19/mo ($12 yearly) for 15 videos of up to 2 minutes. Pro: $39 ($23 yearly). Business: $69 ($41 yearly). "Magic Clips" auto-clipping is a $19/mo add-on. — [overlap.ai](https://overlap.ai/blogs/opusclip-alternatives)
- **Descript.** Free: 60 media min/mo. Hobbyist: about $16–24 for 10 media hours. Creator: about $24–35 for 30 media hours and full access to Underlord (the AI co-editor). Business: about $50–65. Annual billing saves about 35%. — [Sonix](https://sonix.ai/resources/descript-pricing/); [Shade](https://shade.inc/blog/descript-pricing)
- **Screen Studio** (macOS only): $29/mo or $9/mo billed yearly, no free plan. — [Docsie](https://www.docsie.io/vs/screen-studio-vs-cap-pricing/)
- **Cap.** Free open-source local tier. The desktop license is $29/yr or $58 lifetime. Pro cloud is $12/user/mo. It works on both Mac and Windows. — [Docsie](https://www.docsie.io/vs/screen-studio-vs-cap-pricing/)
- **Tella.** 7-day trial, then $13/user/mo. Premium is $19 and adds 60fps export and branding. — [Tella alternatives page](https://www.tella.com/alternatives/screen-studio)
- **HeyGen.** Creator: $29/mo (about $24 annually) with 600 credits, "fewer than 30 minutes of Avatar IV" per month. Pro starts at $49, Business at $149 + $20/seat. — [eesel.ai](https://www.eesel.ai/blog/heygen-pricing); [HeyGen pricing](https://www.heygen.com/pricing)
- **ElevenLabs.** Starter $6, Creator $22 (121k credits; the first tier with Professional Voice Cloning), Pro $99, Scale $299, Business $990. — [eesel.ai / search summary](https://www.eesel.ai/blog/heygen-pricing)
- **Dubbing.** ElevenLabs dubs audio only, with no lip-sync, at about $0.08/min effective. HeyGen video translation includes lip-sync at about 5 credits/min (about $0.48/min) and covers 175+ languages. — [videodubber.ai comparison](https://videodubber.ai/compare/elevenlabs-vs-heygen/); [bibigpt](https://bibigpt.co/blog/posts/ai-video-dubbing-translation-tools-2026-guide). The ElevenLabs dubbing language count ("29") in that source may be outdated.
- **B-roll per-second API pricing (2026)** — [DevTk.AI](https://devtk.ai/en/blog/ai-video-generation-pricing-2026/); [fluxnote](https://fluxnote.io/guides/ai-video-model-pricing-comparison-2026). Sources disagree slightly:
  - Kling: about $0.07/s (Kling 3.0 is about $0.10/s).
  - Veo 3.1: Fast is $0.15–0.20/s. Standard is $0.40/s, and 4K is $0.60/s.
  - Runway Gen-4 / 4.5: about $0.50/s, or plans at $12–95/mo.
- **Sora shutdown.** OpenAI announced on 2026-03-24 that it is discontinuing Sora. The web/app experience ended 2026-04-26 and the API ended 2026-09-24. — [Futurum](https://futurumgroup.com/insights/openai-sora-discontinuation-what-the-end-of-a-platform-means-for-enterprise-ai-strategy/); [Wikipedia](https://en.wikipedia.org/wiki/Sora_(text-to-video_model)); [OpenAI community thread](https://community.openai.com/t/is-the-sora2-api-still-working/1379946). **Any guide recommending Sora for B-roll is outdated.**

### Inferences
- For coding content, B-roll AI video is a nice-to-have. Remotion-rendered code and UI animations are cheaper and more on-topic than Veo or Kling clips.
- HeyGen is the only one-stop option if lip-synced RU dubs of a talking head are needed. For screencast-heavy videos without a visible face, audio-only dubbing (ElevenLabs, or open-source VideoLingo with a cloned voice) is enough and about 6x cheaper.

### Gaps
- No verified 2026 pricing was found for Synthesia, Captions.ai (now "Mirage"?), CapCut Pro, Loom, Rask.ai or Kling/Runway consumer subscriptions.
- The Descript price ranges vary across aggregators. The official page was not fetched.

## Q3. How vibe-coding creators make videos (recording, zooms, code highlighting, Claude Code/Cursor sessions)

### Takeaway
The 2026 pattern is changing. The old way was to record the screen live, then add auto-zoom in Screen Studio or Cap. Increasingly, creators instead record only the talking head plus raw sessions and let Claude Code rebuild the "screen moments" as Remotion code, using fake screencasts, animated code and auto-zoom. For terminal-heavy content (Claude Code CLI), scripted VHS .tape recordings and asciinema give crisp, reproducible terminal footage.

### Cited Findings
- claude-youtube-editor: every screen moment is Remotion TSX composited over the cut. It also includes TTS voice, SFX, thumbnail and YouTube upload. — [GitHub](https://github.com/hassancs91/claude-youtube-editor)
- screencli: Claude Code drives the demo and outputs an MP4 with auto-zoom, click highlights and cursor trails in about 2 minutes. — [screencli](https://screencli.sh/blog/record-product-demos-with-claude-code)
- The Playwright MCP save-video flag can record browser sessions that Claude drives. — [ItachiDevv/claude-screen-recorder](https://github.com/ItachiDevv/claude-screen-recorder)
- Screen Studio remains the Mac reference for auto-zoom and cursor smoothing ($9/mo annual). Cap is the cross-platform, open-source alternative. — [Docsie](https://www.docsie.io/vs/screen-studio-vs-cap-pricing/)
- VHS writes terminal recordings from a declarative script (MIT, 21k stars). — [GitHub](https://github.com/charmbracelet/vhs)

### Inferences
- A practical recipe for a Claude Code / Cursor tutorial:
  1. Record the real session in Screen Studio or Cap, at 1080p/4K with a large font.
  2. Record face-cam separately.
  3. Transcribe with WhisperX.
  4. Have Claude Code do the silence cut (auto-editor) and assemble Remotion overlays: code-diff highlights, captions and chapter cards.
  5. Use VHS to re-shoot any terminal segment cleanly.
- Code highlighting in Remotion is typically done with Shiki or code-hike-style components. This is not verified in this research.

### Gaps
- No direct interviews or breakdowns were found from specific top vibe-coding YouTubers (e.g. which recorder a particular creator uses). YouTube video content was not searchable here.
- No data on Cursor-specific recording plugins.

## Q4. Faceless AI channels: do they work, demonetization risk (YouTube "inauthentic content"), TikTok AI labels

### Takeaway
YouTube's policy is tool-agnostic. AI voice and faceless formats remain monetizable when the script and curation are original. The July 15, 2025 rename from "repetitious" to "inauthentic content" targets templated, mass-produced output, and enforcement escalated to terminations in January 2026. TikTok permits AI content but requires an AIGC label on realistic AI people and scenes, and it auto-labels content via C2PA metadata.

### Cited Findings
- On 2025-07-15 YouTube renamed its "repetitious content" YPP policy to "inauthentic content". It defines this as mass-produced or repetitive content, e.g. "made with a template with little to no variation across videos" or "easily replicable at scale". — [ytgrowth.io](https://ytgrowth.io/blog/youtube-ai-policy); [TechCrunch 2025-07-09](https://techcrunch.com/2025/07/09/youtube-prepares-crackdown-on-mass-produced-and-repetitive-videos-as-concern-over-ai-slop-grows); [Gulf News](https://gulfnews.com/technology/youtube-updates-monetisation-policies-ai-and-repetitive-content-ban-begins-july-15-1.500192660). These are secondary sources. The official page (support.google.com/youtube/answer/1311392) could not be fetched.
- The policy is "tool-agnostic". "AI voiceover means automatic demonetization" is false: "a synthetic voice reading an original script violates nothing". — [ytgrowth.io](https://ytgrowth.io/blog/youtube-ai-policy)
- In a January 2026 enforcement wave, 16 channels with about 35M combined subscribers and 4.7B lifetime views (about $10M/yr in ad revenue) were terminated, not just demonetized. — [ytgrowth.io](https://ytgrowth.io/blog/youtube-ai-policy); [aituber.app](https://aituber.app/blog/faceless-youtube-channels-demonetized-2026/). The same event was covered by the [Hollywood Reporter: "Faceless Creators Take a Hit As YouTube Cracks Down on AI Slop"](https://www.hollywoodreporter.com/business/digital/faceless-creators-youtube-ai-damage-1236617586/) (not fetched; blocked).
- The targeted pattern is "AI voiceover read over generic stock footage, with no commentary, no unique angle, and often multiple near-identical channels run by the same operator". — [aituber.app](https://aituber.app/blog/faceless-youtube-channels-demonetized-2026/)
- **TikTok.** AI content is permitted, but a visible label is required on AI visuals or audio depicting realistic people or scenes. Script writing and other AI text workflows are exempt. TikTok reads C2PA Content Credentials (integrated since January 2025) and auto-applies the AIGC label. Unlabeled realistic AI can be down-ranked or removed, and repeat cases can lead to account suspension. — [cinerads](https://www.cinerads.com/blog/tiktok-ai-content-policy); [storrito](https://storrito.com/resources/tiktoks-2026-ai-labeling-rules-and-what-they-signal-for-platform-governance/). These are secondary sources, not the official TikTok page.

### Inferences
- A vibe-coding channel built on real coding sessions, original scripts and a consistent host (voice or face) is structurally low-risk. The risk comes from MoneyPrinter-style "keyword to stock footage + TTS" automation at volume, and from running multiple near-identical channels.
- YouTube also has a separate disclosure requirement for realistic altered/synthetic content (the "altered or synthetic" toggle, from 2024). It applies to cloned voices or avatars made to look like real people. It was not re-verified here.
- For Shorts cut automatically from your own long-form (OpusClip-style), originality is inherited from the source. That makes it lower risk than generated faceless shorts.

### Gaps
- **Reddit sentiment was not captured directly.** No reddit.com results came back for r/NewTubers, r/youtube, r/VideoEditing, r/n8n, r/SideProject or r/aivideo. The claim that "creators on Reddit report channels wiped overnight" appears only second-hand in aggregator blogs. Many results were SEO or Gumroad "faceless course" pages, which have a conflict of interest.
- The official YouTube and TikTok policy texts were not fetched (proxy blocked).
- No reliable data on the RPM or success rate of faceless channels after the policy change.

## Q5. Recommended minimal-cost vs premium stack (solo creator)

### Takeaway
The minimal stack costs about $0–15/mo. It is built on open-source tools (OBS/Cap free, VHS, faster-whisper, auto-editor, Remotion driven by Claude Code, Kokoro/F5/Chatterbox TTS, VideoLingo for RU) plus one clipper free tier. The premium stack costs about $150–250/mo: Screen Studio + Descript Creator + OpusClip Pro + ElevenLabs Creator + HeyGen Creator, with pay-per-second Veo/Kling for B-roll.

### Cited Findings (price inputs)
- Cap free tier or $58 lifetime; Screen Studio $9/mo annual — [Docsie](https://www.docsie.io/vs/screen-studio-vs-cap-pricing/)
- Remotion is free for individuals and teams of 3 or fewer — [remotion.pro](https://www.remotion.pro/license)
- OpusClip Pro $14.50/mo annual; Vizard Creator $14.50/mo annual; Submagic from $12/mo annual — [overlap.ai](https://overlap.ai/blogs/opusclip-alternatives)
- Descript Creator about $24–35/mo — [Sonix](https://sonix.ai/resources/descript-pricing/)
- ElevenLabs Creator $22; HeyGen Creator $29 ($24 annual) — [eesel.ai](https://www.eesel.ai/blog/heygen-pricing)
- Kling about $0.07/s and Veo 3.1 $0.15–0.40/s — [DevTk.AI](https://devtk.ai/en/blog/ai-video-generation-pricing-2026/)

### Inferences
**Minimal (about $0–15/mo; laptop, optional 8–12 GB GPU):**

| Step | Tools |
|---|---|
| Script | Claude or ChatGPT (existing subscription) |
| Recording | Cap free or OBS; VHS/asciinema for terminal |
| Voice | Your own voice. Or Kokoro (no GPU) / F5-TTS / Chatterbox (MIT) |
| Transcripts & captions | faster-whisper/WhisperX, burned in via Remotion or FFmpeg |
| Cuts | auto-editor |
| Edit & motion | Remotion or Motion Canvas, generated by Claude Code (e.g. the claude-youtube-editor pattern) |
| Shorts | Open-source clipper (AI-Youtube-Shorts-Generator / OpenClipper) or the OpusClip free tier (watermark) |
| EN↔RU | VideoLingo or pyvideotrans + cloned TTS |
| Thumbnails | Image model plus a Remotion still or Figma |

**Premium (about $150–250/mo plus usage):**

| Step | Tools |
|---|---|
| Recording | Screen Studio ($9–29) or Tella |
| Editing | Descript Creator (~$24–35) |
| Clipping & captions | OpusClip Pro ($15–29) or Submagic |
| Voice & dubbing | ElevenLabs Creator ($22) for voice clone and audio dubs |
| Lip-synced RU version / avatar intros | HeyGen Creator ($29) |
| B-roll | Veo 3.1 / Kling per second |

**Avoid:** Sora (discontinued), coqui/XTTS (unmaintained), openscreen (archived) and ClipsAI (abandoned). Also avoid a keyword-to-stock-footage faceless pipeline (inauthentic-content risk).

### Gaps
- There is no single source that benchmarks full end-to-end stacks. The stack totals above are my own arithmetic from the individual price points.
- Thumbnail tooling (e.g. AI thumbnail generators, A/B "Test & Compare" on YouTube) was not researched in depth.
