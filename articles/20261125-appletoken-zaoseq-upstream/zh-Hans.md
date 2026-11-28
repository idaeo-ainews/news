# 2026-11-25 AppleToken 新增上游：造序科技（ZaoSeq）

归档类型：发行者公告的结构化数据。发行者：株式会社和心（AppleToken）。数据日期：2026-11-25（JST）；单价、模型数、容量 2026-11-28 重读。

## 摘要
- 事件：AppleToken API v2.65 新增上游 ZaoSeq（造序科技，台湾）。
- 上游公司：造序科技有限公司（ZaoSeq Technologies Co., Ltd.），2026-10-08 新北市设立；官网 https://zaoseq.com ，GPU 算力服务 https://compute.zaoseq.com
- 指定方式：model 写 `zaoseq/<模型>`。只在指名时使用，不参与 `auto/` 自动选路。

## 模型表（11 月 28 日目录，美元）
| model | 类型 | 单价 |
|---|---|---|
| `zaoseq/qwen3.8-27b-fp8` | 对话 | 每百万 token 输入 0.189、输出 1.259 |
| `zaoseq/qwen3.8-27b-nvfp4` | 对话 | 每百万 token 输入 0.189、输出 1.259 |
| `zaoseq/deepseek-v4-flash-0731` | 对话 | 每百万 token 输入 0.173、输出 0.354 |
| `zaoseq/qwen3-asr` | 语音转文字 | 每秒音频 0.00003（约每小时 0.108） |
| `zaoseq/flux-2-klein-4b` | 文生图 | 每张 0.0045 |
| `zaoseq/minimax-h3` | 视频 | 每秒视频 0.0068 起，最高 0.0837 |

六个模型 2026-11-28 状态均为 active／normal。Qwen3.8 27B 有 FP8 和 NVFP4 两版（NVFP4 在 11-25 上线后加入），两者同价，不做价格比较。

## 规格
- 两个对话模型：输出上限 8,192 tokens，默认 2,048。
- Qwen3-ASR：`POST /v2/audio/transcriptions`。
- FLUX.2 klein 4B：512×512、768×768、1024×1024；一次 1 张；最多 4 张输入图；可指定 seed；无水印。
- MiniMax H3：352p、480p、720p、768p、1080p、1440p；16:9、9:16；一律含音频；5–15 秒（1080p、1440p 最长 10 秒）；最多 3 张参考图；质量目前开放 light、medium。

## 容量规则
- 每个密钥同时 16 个请求、每分钟 300 个；视频与其他请求共用“同时 16 个”。
- 对话、图片、语音转文字：同一条连接排队，最长约 60 秒；排不上返回 429（带 Retry-After，可重试，不扣点数）；排队期间不报价、不冻结点数。
- 视频：按任务排队（queued），最长 60 分钟；超时 failed（upstream_busy），冻结额度全部退回。

## 目录内对比（11 月 28 日目录）
- DeepSeek V4 Flash 经造序，输出每百万 token 0.354 美元，是目录中提供该模型的三个上游里最低的。

## MiniMax H3 产品条件（MiniMax H3 Community License，照原文列出）
- 不向欧盟、英国、韩国、美国的用户提供。
- 不得用输出训练其他 AI 模型。
- 公开发布时请标注为 AI 生成。

## 来源与边界
- AppleToken 版本记录 API v2.65；模型目录 GET /v2/models（2026-11-25、2026-11-28 实读）；AppleToken 文档。
- 单价会变动，以实时目录为准。

人类可读正本：https://km.idaeo.ai/post/ai/appletoken-zaoseq-upstream-20261125?lang=zh-Hans&utm_source=github_news&utm_medium=article&utm_campaign=zaoseq-launch&utm_content=ZSQ-github_news-zh-Hans

联系：appletoken@washinmura.jp

ZSQ-github_news-zh-Hans
