# AI Content Engine Pipeline — Discovery Report

**Brand:** Innovative Hype  
**Author:** Micah 'Geo' Peoples | @innovativehype  
**Date:** 2026-05-14  
**Status:** Research complete — Phase 1 of 3 (D1)

---

## 1. Brand Audit

### Overview
Innovative Hype is a **7-year-old Substack publication** by Micah 'Geo' Peoples. The tagline: "Innovative Hype keeps you ahead of the innovative technology & trends shaping our culture." (Note: the Substack page currently has a typo: "the the").

### Content Analysis

**Cadence:** Highly sporadic. The archive reveals large multi-month gaps between posts:

| Date | Post |
|------|------|
| Nov 2025 | Gambling Crackdown Rocks the NBA, AWS Stumbles, MTV's Music Era Ends |
| Oct 2025 | Prediction Markets Go Mainstream, AI Dominates GDP Growth, The Middle Class At Risk |
| Jun 2025 | AI & The Social Contract: Competing Visions For Our Future |
| Oct 2024 | Innovative Hype Roundup September 2024 |
| Jan 2024 | The Case for Microeconomies + CFB piece |
| Aug 2023 | Messi/MLS analysis |
| Jul 2023 | Podcast episodes 001-004 (Web3, Creativity, Arweave, NFTs) |

Earlier years (2019-2023) had more frequent posting, including podcasts and regular roundups. Content has nearly dried up in 2024-2025.

**Tone & Style:**
- Conversational, opinionated, first-person
- Cultural commentary weaving tech, sports, and society
- Long-form analysis (~1,500-2,500 words per post)
- "Roundup" format for news aggregation posts
- Uses section headers, inline links, and rich formatting

**Topics Covered:**
- AI/tech trends (AI & GDP, AI social contract)
- Sports (NBA, NFL, MLS)
- Web3/crypto (NFTs, Arweave, DeFi)
- Economics (prediction markets, microeconomies)
- Media/culture (MTV, content consumption)

**Engagement Metrics:**
- Extremely low: **0-3 likes per post, 0-1 comments**
- Subscriber count not publicly visible
- No paid subscription tier visible

**Brand Identity:**
- No logo or visual branding beyond the text "Innovative Hype"
- No custom domain (innovativehype.com has broken SSL — likely abandoned)
- Social presence: Twitter, Instagram links on Substack
- No apparent brand colors, style guide, or visual identity
- The Substack uses the default template with no customization

### Brand Audit Takeaways
1. **The brand is dormant** — content velocity is near-zero
2. **AI theme is emerging** — 3 of the last 4 posts touch AI
3. **Voice is the asset** — Micah's conversational, cross-domain style is distinctive
4. **No visual identity exists** — greenfield for branding
5. **Automation is justified** — manual posting isn't happening; automated content could revive the publication

---

## 2. AI News Research Tools

### Top Options (ranked by feasibility)

#### 2.1 RSS Feeds (Recommended Primary Source)
**Best for:** Zero-cost, reliable, always-on news aggregation.

Top AI news sources with RSS:
- **TechCrunch AI:** `https://techcrunch.com/category/artificial-intelligence/feed/`
- **The Verge AI:** `https://www.theverge.com/ai-artificial-intelligence/rss/index.xml`
- **ArXiv CS.AI:** `https://rss.arxiv.org/rss/cs.AI`
- **MIT Technology Review AI:** RSS available
- **VentureBeat AI:** `https://venturebeat.com/category/ai/feed/`
- **Hacker News:** Algolia API for AI-tagged stories
- **Simon Willison's Blog:** High-signal AI commentary
- **Import AI (Jack Clark):** Weekly newsletter with RSS

**Feasibility:** ✅ Free, no API keys, rate-limit friendly, Python `feedparser` library handles everything.

#### 2.2 NewsAPI
- **URL:** `https://newsapi.org`
- **Free tier:** 100 requests/day, 3-day article history
- **Paid:** $449/mo for 30-day history, 250 req/15min
- **Verdict:** ⚠️ Free tier too limited for daily automation (only 3-day window). Paid tier expensive.

#### 2.3 Perplexity API
- **URL:** `https://docs.perplexity.ai`
- **Pricing:** Pay-per-request (Sonar models). ~$1 per 1,000 queries.
- **Use case:** Summarize news, not aggregate it. Can be called on-demand to summarize/article a batch of RSS items.
- **Verdict:** ✅ Good for the "rewrite/editorialize" stage, not for raw aggregation.

#### 2.4 GitHub Community Projects
Relevant open-source aggregators found:

| Project | Stars | License | Notes |
|---------|-------|---------|-------|
| ai-news-daily/ai-news-daily | 11 | none | Crawls 50+ sources, local LLMs, deploys to GitHub Pages |
| AKAlSS/AI-News-Aggregator | 12 | none | Python, RSS-based, AI topic filtering |
| hoangsonww/AI-Gov-Content-Curator | 28 | MIT | End-to-end: crawl → summarize → newsletter |
| Adinath-Jagtap/blog-automation | 8 | none | 15+ sources, Gemini 2.5 rewrite, auto-publish |

**Verdict:** These are small/personal projects. Better to build a simple custom pipeline using feedparser + LLM summarization.

### Recommended Approach
```
RSS Feeds (20+ sources) → Filter by AI keywords → LLM summarization (Hermes) → Newsletter draft
```
Free, simple, maintainable. No external API dependencies except the LLM.

---

## 3. Video Generation Tools

### Top 3 Evaluated

#### 3.1 MoneyPrinterTurbo ⭐ 57,190
- **URL:** `https://github.com/harry0703/MoneyPrinterTurbo`
- **License:** MIT
- **Updated:** May 2026 (actively maintained)
- **Language:** Python
- **What it does:** One-click AI video generation from text. Input a topic/script → outputs a finished short video with AI voiceover, subtitles, and stock footage / AI-generated visuals.
- **Strengths:** Massive community, MIT license, battle-tested, Chinese + English support, faceless video format
- **Weaknesses:** Chinese-first documentation, requires API keys for LLM/TTS (OpenAI, Azure, etc.)
- **Best for:** Rapid faceless short-form video production

#### 3.2 Open-Generative-AI ⭐ 13,391
- **URL:** `https://github.com/Anil-matcha/Open-Generative-AI`
- **License:** None (no explicit license — use caution)
- **Updated:** May 2026
- **What it does:** Web-based AI studio with 200+ models (Flux, Midjourney-style, Kling, Sora, Veo). Image + video generation. Self-hosted.
- **Strengths:** All-in-one, no content filters, huge model selection, web UI
- **Weaknesses:** No license (legal risk), more of a creative studio than automated pipeline, heavy GPU requirements
- **Best for:** Manual/semi-automated visual content creation

#### 3.3 Toonflow ⭐ 7,917
- **URL:** `https://github.com/HBAI-Ltd/Toonflow-app`
- **License:** Apache 2.0
- **Updated:** May 2026
- **What it does:** Converts stories/scripts into animated short dramas. AI scriptwriting → storyboarding → character generation → video.
- **Strengths:** Apache 2.0, full pipeline, desktop app
- **Weaknesses:** Chinese-first, animation-focused (may not match news-style content), complex setup
- **Best for:** Story-driven animated content (not news/punditry format)

### Other Notable Tools

| Tool | Stars | License | Notes |
|------|-------|---------|-------|
| Generative-Media-Skills | 3,227 | MIT | Agent-based media gen for Claude Code/Cursor |
| forge-film | 654 | MIT | Multi-model parallel film generation |
| Clipify | 3 | MIT | Long-form → short clip extraction |
| ai-slop-pipeline-tiktoker | 38 | none | CLI for automated TikTok/Shorts/Reels |
| ai-video-automation | 3 | none | Seedance + Wavespeed + Fal AI pipeline |

### Recommendation

**MoneyPrinterTurbo** is the clear winner for automated short-form video:
- MIT license, 57K stars, active community
- Designed for exactly this use case (automated short video from text)
- Faceless format fits the news/punditry niche
- Can pair with Hermes for script generation
- Forks like MoneyPrinterAICreate add Wan2.1 text-to-video for richer visuals

**Architecture:**
```
Hermes (script generation) → MoneyPrinterTurbo (video rendering) → Distribution APIs
```

---

## 4. Distribution APIs

### 4.1 YouTube Shorts (YouTube Data API v3)
- **Status:** ✅ Fully supported
- **Auth:** OAuth 2.0 (Google Cloud Console app required)
- **Quota:** 10,000 units/day free (1 video upload ≈ 1,600 units)
- **Rate limit:** ~6 video uploads/day on free quota
- **Upload process:**
  1. POST `https://www.googleapis.com/upload/youtube/v3/videos`
  2. Set `videoCategoryId` and metadata
  3. Videos under 60s with vertical aspect ratio auto-classify as Shorts
- **App Review:** No special review needed for basic uploads
- **Verdict:** ✅ Most accessible. Free quota sufficient for daily 1-video pipeline. Best starting point.

### 4.2 TikTok (Content Posting API)
- **Status:** ✅ Available but restricted
- **URL:** `https://developers.tiktok.com/products/content-posting-api`
- **Auth:** OAuth 2.0 (TikTok for Developers app)
- **Requirements:**
  - TikTok developer account + approved app
  - App must pass TikTok's review process
  - `video.publish` permission scope (may be restricted to approved partners)
  - Usage is monitored; TikTok has been known to limit API access aggressively
- **Upload process:**
  1. `POST /v2/post/publish/video/init/` — initialize upload
  2. Upload video chunks
  3. `POST /v2/post/publish/video/complete/` — finalize
- **Verdict:** ⚠️ Highest friction. TikTok is known for restrictive API access. May require manual posting or using their web-based Creator tools instead.

### 4.3 Instagram Reels (Instagram Platform / Facebook Graph API)
- **Status:** ✅ Supported
- **URL:** `https://developers.facebook.com/docs/instagram-platform/content-publishing`
- **Auth:** OAuth 2.0 via Facebook Login
- **Requirements:**
  - Instagram Professional Account (Business or Creator)
  - Connected to a Facebook Page
  - Page Publishing Authorization (PPA) — new requirement as of 2025
  - `instagram_content_publish` permission
  - App Review required for `instagram_content_publish`
- **Upload process (2-step):**
  1. `POST /{IG_USER_ID}/media` — create media container with video URL, caption, thumb
  2. `POST /{IG_USER_ID}/media_publish` — publish the container
- **Key constraints:**
  - Media must be publicly accessible URL (not direct upload)
  - Reels: max 90 seconds, 9:16 aspect ratio
  - App must pass Meta App Review (can take days to weeks)
- **Verdict:** ⚠️ Medium friction. API works but requires FB Page setup + App Review. PPA adds a new hurdle.

### 4.4 Substack
- **Status:** ❌ No official API
- **Publishing method:** Email-based only
  - Each Substack publication has a unique `@substack.com` email address
  - Email subject → post title, email body → post content
  - Supports Markdown in email body
  - Can schedule posts via email (add date to subject line)
- **Alternative (unofficial):** Reverse-engineered internal APIs exist but are fragile and violate ToS
- **Verdict:** ⚠️ Email-based publishing works but is brittle. No programmatic draft management, no analytics API, no media upload API. Best approach: use SMTP via Python to send formatted emails to the Substack publishing address.

### Distribution Feasibility Matrix

| Platform | API Available | Auth Type | Free Tier Viable | Automation Difficulty |
|----------|--------------|-----------|-----------------|----------------------|
| YouTube Shorts | ✅ Full | OAuth 2.0 | ✅ Yes (6 videos/day) | Low |
| TikTok | ⚠️ Restricted | OAuth 2.0 | ✅ Yes | High |
| Instagram Reels | ⚠️ Partial | OAuth 2.0 + FB | ✅ Yes | Medium |
| Substack | ❌ None (email) | Email token | ✅ Yes | Low-Medium |

---

## 5. Substack API Deep-Dive

### Current State (May 2026)
Substack has **no public API** for content publishing. The platform is deliberately closed.

### Email-Based Publishing (The Only Reliable Method)
1. Each publication gets a secret `@substack.com` posting address
2. Send email → Substack converts to post
3. Subject line = post title
4. Body (Markdown supported) = post content
5. Schedule by adding date to subject: `[Schedule: 2026-05-20 09:00]`

**Implementation via SMTP:**
```python
import smtplib
from email.mime.text import MIMEText

msg = MIMEText(markdown_body, 'plain')
msg['Subject'] = post_title
msg['From'] = sender_email
msg['To'] = 'innovativehype@substack.com'  # secret posting address
```

### Limitations
- No draft preview/review before publishing
- No programmatic editing of published posts
- No analytics retrieval
- No subscriber management via API
- No image upload — images must be hosted elsewhere and linked
- Email-based method can be flaky (spam filters, delays)

### RSS Feed (Read-Only)
- `https://innovativehype.substack.com/feed` — public RSS of published posts
- Useful for monitoring but not for publishing

---

## 6. Automation & Cron Strategy

### Option A: Hermes Cron Jobs (Recommended)
Hermes has built-in cron job support. This is the most integrated approach:

- **Direct LLM access:** Hermes agents can generate scripts, summaries, and content in the same runtime
- **Tool integration:** Same tools available (terminal, web, file, browser) as interactive sessions
- **Skill loading:** Can load skills for specific pipeline stages
- **Delivery:** Auto-deliver results to any connected channel
- **Chaining:** `context_from` allows pipeline stages (collect → summarize → publish)
- **Monitoring:** Built-in heartbeat, timeout, retry logic
- **Schedule:** Supports cron expressions and human-readable intervals

**Pipeline structure:**
```
Job 1 (daily, 6am):    "Aggregate AI news from RSS feeds" → /tmp/news_batch.json
Job 2 (daily, 6:30am): "Summarize and draft newsletter" → email draft
Job 3 (daily, 7am):    "Generate short-form video script" → script.md
Job 4 (daily, 7:30am): "Render video via MoneyPrinterTurbo" → video.mp4
Job 5 (daily, 8am):    "Distribute to YouTube/Substack" → published
```

### Option B: GitHub Actions
- Free for public repos, 2,000 min/month for private
- Good for git-triggered workflows
- Less suited for LLM-heavy pipelines (no native LLM access)
- Requires self-hosted runner or external API calls for AI

### Option C: External Scheduler
- macOS `launchd` — reliable for local-only, no cloud
- n8n (self-hosted) — visual workflow, good for multi-step pipelines
- Cron (Unix) — simplest, no dependencies

### Recommendation
**Hermes cron jobs** are the clear winner: they have native LLM access, the same toolset, built-in monitoring, and can chain stages via `context_from`. No external infrastructure needed. Start with one daily job and expand.

---

## 7. Recommended Architecture

### Three-Phase Pipeline

```
PHASE 1: AGGREGATION (daily, 6am)
├── 20+ AI RSS feeds → feedparser
├── Filter: AI/ML/tech keywords
├── Deduplicate across sources
└── Output: 10-15 curated stories → /tmp/news_batch.json

PHASE 2: CONTENT GENERATION (daily, 7am)
├── Newsletter: Hermes drafts ~800-word roundup
│   └── Tone match: Innovative Hype conversational style
│   └── Publish: SMTP email to Substack
├── Video Script: Extract top 3 stories → 60s script
│   └── Output: script.md with timestamps
└── Video Render: MoneyPrinterTurbo
    └── Input: script.md + AI voiceover + stock visuals
    └── Output: short.mp4 (vertical, 60s)

PHASE 3: DISTRIBUTION (daily, 8am)
├── YouTube Shorts: YouTube Data API v3
├── Instagram Reels: Facebook Graph API (after App Review)
├── TikTok: Content Posting API (if approved)
└── Substack Newsletter: already published in Phase 2
```

### Phased Roadmap

| Phase | Scope | Timeline | Dependency |
|-------|-------|----------|------------|
| P0: MVP | RSS → Newsletter (Hermes → Substack email) | 1-2 days | None |
| P1: Video | Newsletter → Script → MoneyPrinterTurbo → MP4 | 2-3 days | P0 complete |
| P2: YouTube | Video → YouTube Shorts API upload | 1 day | P1 complete, Google Cloud app |
| P3: Instagram | Video → Instagram Reels API | 3-5 days | P1 complete, FB App Review |
| P4: TikTok | Video → TikTok API | 1-2 weeks | P1 complete, TikTok App Review |
| P5: Enhance | Multi-platform, A/B testing, analytics | Ongoing | All prior |

### Technology Stack

| Component | Tool | License | Cost |
|-----------|------|---------|------|
| News aggregation | feedparser (Python) | BSD | Free |
| LLM (content gen) | Hermes via OpenRouter | — | API usage |
| Video rendering | MoneyPrinterTurbo | MIT | LLM API keys |
| TTS (voiceover) | OpenAI TTS / Edge TTS | — | ~$0.015/1K chars |
| YouTube upload | Google API Python Client | Apache 2.0 | Free (quota) |
| Substack publish | smtplib (stdlib) | PSF | Free |
| Automation | Hermes cron jobs | Built-in | Free |
| Hosting | Local macOS / Hermes | Built-in | Free |

### Estimated Monthly Cost
- LLM API (OpenRouter): ~$5-10/month (1 newsletter + 1 video script daily)
- TTS API: ~$1/month
- YouTube API: Free (within quota)
- **Total: ~$6-11/month**

---

## 8. Key Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|------------|
| Substack email publishing unreliable | Newsletter doesn't publish | Add verification step (check RSS feed after send) |
| TikTok API access denied | Can't automate TikTok | Manual posting fallback; prioritize YouTube |
| Instagram App Review rejected | Can't automate Reels | Start with YouTube-only; re-apply with stronger use case |
| MoneyPrinterTurbo API costs spike | Budget overrun | Cap monthly API spend; use local models where possible |
| Brand voice mismatch (AI vs. Micah) | Content feels inauthentic | Fine-tune prompts with existing posts as examples; human review gate |
| Copyright issues with news aggregation | Legal risk | Summarize/transform, don't republish verbatim; link to sources |

---

## 9. Immediate Next Steps

1. **Set up RSS aggregation script** — Python, feedparser, 20+ AI sources
2. **Create Hermes skill** for "Innovative Hype newsletter draft" — tone-matched prompt with existing posts as few-shot examples
3. **Configure Substack email publishing** — SMTP to secret posting address
4. **Install MoneyPrinterTurbo** — test with a sample script
5. **Create YouTube/Google Cloud project** — OAuth setup for Shorts upload

---

_Research conducted 2026-05-14 for Hermes Kanban task t_124f75d6. No code implemented — discovery phase only._
