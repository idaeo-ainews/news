# 2026-11-25 AppleToken adds upstream: ZaoSeq (造序科技)

Archive type: structured data from an issuer announcement. Issuer: 株式会社和心 (AppleToken). Data date: 2026-11-25 (JST); prices, model count and capacity re-read on 2026-11-28.

## Summary
- Event: AppleToken API v2.65 added the upstream ZaoSeq (造序科技, Taiwan).
- Upstream company: 造序科技有限公司 (ZaoSeq Technologies Co., Ltd.), incorporated in New Taipei City on 2026-10-08; website https://zaoseq.com , GPU compute service https://compute.zaoseq.com
- How to select: set model to `zaoseq/<model>`. Used only when named; not part of `auto/` routing.

## Model table (November 25 catalog, USD)
| model | type | price |
|---|---|---|
| `zaoseq/qwen3.8-27b-fp8` | chat | 0.236 input / 1.574 output per million tokens |
| `zaoseq/qwen3.8-27b-nvfp4` | chat | 0.236 input / 1.574 output per million tokens |
| `zaoseq/deepseek-v4-flash-0731` | chat | 0.216 input / 0.443 output per million tokens |
| `zaoseq/qwen3-asr` | speech to text | 0.00003 per second of audio (about 0.108 per hour) |
| `zaoseq/flux-2-klein-4b` | text to image | 0.0045 per image |
| `zaoseq/minimax-h3` | video | from 0.0068 per second, up to 0.0837 |

Limited-time 20% off: from November 27 to November 30, 23:59, DeepSeek V4 Flash and both Qwen3.8 27B builds are 20% off. During that window the catalog price (USD per million tokens) is 0.173 input / 0.354 output for DeepSeek V4 Flash and 0.189 input / 1.259 output for Qwen3.8 27B.

All six showed status active / normal on 2026-11-28. Qwen3.8 27B comes in FP8 and NVFP4 builds (NVFP4 added after the 11-25 launch) at the same price. Their names differ from other versions in the catalog, so no price comparison is made.

## Specs
- Chat models: output limit 8,192 tokens, default 2,048.
- Qwen3-ASR: `POST /v2/audio/transcriptions`.
- FLUX.2 klein 4B: 512×512, 768×768, 1024×1024; 1 image per request; up to 4 input images; seed supported; no watermark.
- MiniMax H3: 352p, 480p, 720p, 768p, 1080p, 1440p; 16:9 and 9:16; audio always included; 5 to 15 seconds (1080p and 1440p up to 10 seconds); up to 3 reference images; quality levels currently open: light, medium.

## Capacity rules
- 16 concurrent requests and 300 requests per minute per key (4 and 60 at the 2026-11-25 launch). Video shares the "16 concurrent" limit with other requests, with at most 3 videos at a time.
- Chat, image, speech to text: queued on the same connection for up to about 60 seconds; if no slot opens, 429 with Retry-After (retryable, no credits deducted); nothing is quoted or frozen while waiting.
- Video: queued as a task (queued) for up to 60 minutes; on timeout, failed (upstream_busy) and the full frozen amount is refunded.

## Comparisons inside the catalog (November 25 catalog)
- DeepSeek V4 Flash via ZaoSeq: 0.443 USD per million output tokens, the lowest among the three upstreams offering this model.

## MiniMax H3 product conditions (MiniMax H3 Community License, as stated)
- Not available to users in the European Union, the United Kingdom, South Korea, or the United States.
- Outputs may not be used to train other AI models.
- Mark publicly released outputs as AI-generated.

## Sources and limits
- AppleToken changelog API v2.65; model catalog GET /v2/models (read on 2026-11-25 and 2026-11-28); AppleToken docs.
- Prices change; the live catalog is authoritative.

Human-readable source: https://km.idaeo.ai/post/ai/appletoken-zaoseq-upstream-20261125?lang=en&utm_source=github_news&utm_medium=article&utm_campaign=zaoseq-launch&utm_content=ZSQ-github_news-en

Contact: appletoken@washinmura.jp

ZSQ-github_news-en
