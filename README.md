<div align="center">

# Kopi.video

**Paste a reference. Get an original UGC ad — with your product and an AI actor.**

[Website](https://kopi.video) · [Pricing](https://kopi.video/pricing) · [Docs](https://kopi.video/docs) · [Blog](https://kopi.video/blog)

<img src="https://kopi.video/brand/og-default.png" alt="Kopi.video — AI UGC video generator" width="760" />

<sub>Status: Beta · Built on Cloudflare · MIT licensed</sub>

</div>

---

## What is Kopi.video?

Kopi.video is an **AI UGC ad generator for e-commerce and growth teams**. It turns a short-form video you have the rights to use into an original 9:16 ad for your product.

Instead of asking a model to "make something like this," Kopi first maps the reference: the hook, pacing, scene order, script beats, and CTA. You review that plan — including the AI actor, model, and credit estimate — and only then does it generate. The result is a new ad with your product and an AI actor, not a copy of the original footage.

> This repository is the public product home for Kopi.video: the story, the screenshots, and the build notes. The application code is maintained separately.

## Why we built it

UGC-style ads work because they feel native, specific, and human. But making them is still slow and expensive:

- A single creator-led UGC ad often costs **$150–$500** and takes days to coordinate.
- Teams can see that a competitor's ad works, but can't explain **why** — the hook, the beat timing, the scene order.
- Most AI video tools start from a blank prompt. You get a generic clip, not a structure that already works.
- Many tools charge before you can judge the plan. One bad generation burns credits and time.
- Fixing one bad scene usually means regenerating the whole video.

Kopi is our answer: **start from a reference, approve the plan, then generate — and only redo what needs work.**

## How it works

1. **Bring a starting point.** Paste a TikTok, Douyin, Instagram Reels, YouTube Shorts, X, Xiaohongshu, Kuaishou, or Weibo link you have the rights to use. Or upload an MP4/MOV, a product photo, or a short brief.
2. **Kopi maps the structure.** The agent identifies the hook, pacing, scene beats, script, and CTA — the parts that make the reference work.
3. **Review the plan.** You see the scenes, AI actor, model, duration, and credit estimate. Nothing is charged until you approve.
4. **Generate and refine.** Kopi produces a 9:16 video with native lip-synced voice and captions. If one scene is wrong, redo that scene and keep the rest.

| Input | Output |
|---|---|
| A reference video, product photo, or product brief | A 9:16 UGC-style ad |
| Your product, script direction, and actor choice | 10s or 15s scenes with native voice and captions |
| An approved plan | A downloadable MP4, with scene-level versions |

## What makes Kopi different

| | Typical AI video tool | Kopi.video |
|---|---|---|
| **Starting point** | A blank prompt | A reference you already trust |
| **What gets reused** | Style or vibes | Hook, pacing, scene structure |
| **Cost control** | Pay per generation | Approve the plan before credits are spent |
| **Editing** | Regenerate the whole video | Redo one scene, keep the rest |
| **AI actor** | Random or generic | A cast of AI actors; keep the same face across videos |
| **Output** | Variable | 9:16, 10s/15s scenes, native lip-sync, captions |

## What we built

### Product

- **A conversational Studio.** One chat thread takes you from idea to plan, generation, and revisions. Sessions survive refreshes and can be resumed.
- **Reference-led ad planning.** The agent breaks a reference into hook, pacing, scenes, audio direction, and CTA, then turns it into an inspectable plan.
- **Plan-first credits.** The plan card is the only paid entry point. Credits are charged after approval; failed generations are refunded automatically.
- **A real AI cast.** 17 AI actors, each designed to keep the same face from scene to scene. You can also create your own actor from a description or a photo you have the rights to use.
- **Character swap.** Put an actor, animal, 3D character, or mascot into an existing 5–25 second video while keeping the original motion, camera, and background.
- **Long-video remake.** Rebuild a longer reference shot by shot, with a look photo and frame-by-frame approval before generation.
- **Scene-level editing.** Redo a single scene, adjust the timeline, and keep every generation as a version.
- **15 ad structures.** Product in hand, unboxing, POV hook, before/after, problem–solution, routine, three reasons, skeptic-turned-fan, obsession scale, street interview, remix, tutorial, sensory food & drink, character swap, and long-video remake.
- **AI content labeling.** Generated media is labeled by default, and outputs can be verified.

### Platform

- **Cloudflare-native.** Workers, Durable Objects, D1, R2, Workflows, and Containers — no separate origin server to babysit.
- **Long-running generation that survives.** Workflows own the paid pipeline: charge, first frame, video generation, polling, voice, render, callback, and refund on failure.
- **Provider abstraction.** Models are selected by capability, not hard-coded into templates. New models can be added without rewriting the product flow.
- **Billing and credits.** Stripe subscriptions, 30-day passes, idempotent credit ledgers, and automatic refunds for failed generations.
- **SSR and machine-readable SEO.** Server-rendered pages, canonical URLs, sitemap, structured data, `llms.txt`, and 55 public URLs across formats, use cases, comparisons, guides, and blog posts.
- **Tests and CI.** TypeScript, Vitest, Playwright, and GitHub Actions cover the core flows, route metadata, and UI breakpoints.

### A few numbers

| Number | What it is |
|---:|---|
| **15** | Ad structures in the template library |
| **17** | AI actors in the current cast |
| **8** | Reference platforms supported by link |
| **55** | Public URLs in the sitemap |
| **3** | Plans: Starter, Pro, Scale |
| **150** | Free credits for a new account |
| **1** | Rule that matters: approve the plan before spending |

## A look at the workflow

| Reference | Your remake |
|---|---|
| <img src="https://kopi.video/landing/examples/product-in-hand-reference.webp" alt="Illustrative product-in-hand reference frame" width="280" /> | <img src="https://kopi.video/landing/examples/heating-belt-remake-poster.webp" alt="AI-generated product-in-hand remake made with Kopi" width="280" /> |
| *Illustrative reference* | *AI-generated with Kopi* |

The structure stays. The product, actor, script, and footage become yours.

## Under the hood

| Layer | Stack |
|---|---|
| Frontend / SSR | TanStack Start, React 19, Tailwind CSS 4 |
| API | Hono on Cloudflare Workers |
| Sessions | Durable Objects with WebSocket hibernation |
| Data | D1 (users, credits, generations, sessions) |
| Media | R2 (uploads, references, frames, segments, renders) |
| Long-running work | Cloudflare Workflows |
| Rendering | Cloudflare Containers + FFmpeg |
| Agent | Pi agent loop with tool calling |
| Models | Gemini for planning and video understanding, MiniMax H3 for video, GPT Image 2 for images |
| Billing | Stripe subscriptions and 30-day passes |
| Tests | Vitest, Playwright, GitHub Actions |

## Current status

Kopi.video is in **beta**. Real generation is open to registered users.

| Item | Status |
|---|---|
| Free trial | 150 credits on signup, no card required |
| Plans | Starter $29 / 2,900 credits · Pro $59 / 6,000 · Scale $119 / 12,500 |
| 30-day passes | $35 / $69 / $139 (Alipay availability pending) |
| Reference links | TikTok, Douyin, Instagram Reels, YouTube Shorts, X, Xiaohongshu, Kuaishou, Weibo |
| Uploads | MP4, MOV, product photos |
| Output | 9:16; 768p standard/fast, 960p cinema |
| Billing | Stripe checkout live; full payment verification still in progress |
| AI labeling | On by default; paid plans can manage the label in Settings. Outputs can be verified |

> Prices and credit costs change as models change. Check [kopi.video/pricing](https://kopi.video/pricing) for the current numbers.

## What's next

- Batch variants, so teams can test more hooks and actors from one approved plan.
- API, MCP, and CLI access for agencies and growth teams.
- More models, higher resolution, and better long-video handling.
- More templates and finer actor controls.
- A better Chinese-language experience for cross-border sellers.

We ship in small, verifiable steps. If a capability is not live, it does not belong in the product copy.

## Principles

- **Structure, not theft.** Use references you have the rights to use. Kopi rebuilds the structure; it does not copy the original footage, music, or script.
- **Approve before spend.** The plan is the contract. Credits are charged only after you say yes.
- **Label AI content.** AI-generated media should be recognizable and verifiable.
- **Keep the human in the loop.** The agent plans; you decide.
- **Be honest about limits.** AI video is not a magic button. The product should show what it can and cannot do.

## Links

| | |
|---|---|
| Website | [kopi.video](https://kopi.video) |
| Pricing | [kopi.video/pricing](https://kopi.video/pricing) |
| Docs | [kopi.video/docs](https://kopi.video/docs) |
| Blog | [kopi.video/blog](https://kopi.video/blog) |
| For AI agents | [kopi.video/llms.txt](https://kopi.video/llms.txt) |
| Deep dive (Chinese) | [How Kopi works](docs/zh/how-kopi-works.md) |
| Contact | [hello@kopi.video](mailto:hello@kopi.video) |

## 中文简介

Kopi.video 是一个面向电商卖家的 **AI UGC 广告生成器**：粘贴一条你有权使用的参考视频，Kopi 拆出它的 hook、节奏和镜头结构，再用你的产品、脚本和 AI 演员重做成一条 9:16 广告。你先看方案，确认后才扣 credits；生成后可以只重做一场，不用整条重来。

我们做了这些事：

- 对话式 Studio：从需求、方案、生成到修改，都在一个会话里完成。
- 参考视频拆解：支持 TikTok、抖音、Reels、Shorts、X、小红书、快手、微博链接，也支持 MP4/MOV 上传。
- 方案卡与积分门禁：方案里写清演员、模型、时长和积分，批准后才扣费；失败自动退款。
- 17 个 AI 演员：同一张脸可以跨视频保持一致，也可以用自己的照片创建演员。
- 换人与长视频复刻：把演员换进现有视频，保留原片动作/镜头/背景；长视频按镜头逐段复刻。
- 单场景重做与版本历史：只改错的那一场，保留其他镜头和旧版本。
- 15 种广告结构/工作流：product in hand、unboxing、POV hook、before/after、routine、street interview 等。
- Cloudflare 全栈：Workers、Durable Objects、D1、R2、Workflows、Containers + FFmpeg。
- SEO/GEO 基础：SSR、sitemap、结构化数据、`llms.txt`，以及 55 个公开 URL。
- AI 标识与验证：生成内容默认带 AI 标识，并提供验证入口。

深入阅读：[从一条参考视频到一条新广告：Kopi 的视频复刻原理](docs/zh/how-kopi-works.md)

## License

MIT. See [LICENSE](LICENSE).
