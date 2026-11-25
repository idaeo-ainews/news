# 2026-11-25 AppleToken 新增上游：造序科技（ZaoSeq）

歸檔類型：發行者公告的結構化資料。發行者：株式会社和心（AppleToken）。資料日期：2026-11-25（JST）。

## 摘要
- 事件：AppleToken API v2.65 新增上游 ZaoSeq（造序科技，台灣）。
- 上游公司：造序科技有限公司（ZaoSeq Technologies Co., Ltd.），2026-10-08 新北市設立；官網 https://zaoseq.com ，GPU 算力服務 https://compute.zaoseq.com
- 指定方式：model 寫 `zaoseq/<模型>`。只在指名時使用，不參與 `auto/` 自動選路。

## 模型表（11 月 25 日目錄，美元）
| model | 類型 | 單價 |
|---|---|---|
| `zaoseq/qwen3.8-27b-fp8` | 對話 | 每百萬 token 輸入 0.236、輸出 1.574 |
| `zaoseq/deepseek-v4-flash-0731` | 對話 | 每百萬 token 輸入 0.216、輸出 0.443 |
| `zaoseq/qwen3-asr` | 語音轉文字 | 每秒音訊 0.00003（約每小時 0.108） |
| `zaoseq/flux-2-klein-4b` | 文字生圖 | 每張 0.0045 |
| `zaoseq/minimax-h3` | 影片 | 每秒影片 0.0068 起，最高 0.0837 |

五個模型 2026-11-25 狀態皆 active／normal。Qwen3.8 27B 是 FP8 版，不做價格比較。

## 規格
- 對話兩模型：輸出上限 8,192 tokens，預設 2,048。
- Qwen3-ASR：`POST /v2/audio/transcriptions`。
- FLUX.2 klein 4B：512×512、768×768、1024×1024；一次 1 張；最多 4 張輸入圖；可指定 seed；無浮水印。
- MiniMax H3：352p、480p、720p、768p、1080p、1440p；16:9、9:16；一律含音訊；5–15 秒（1080p、1440p 最長 10 秒）；最多 3 張參考圖；品質目前開放 light、medium。

## 容量規則
- 每把金鑰同時 4 個請求、每分鐘 60 個；影片與其他請求共用「同時 4 個」。
- 對話、圖片、語音轉文字：同一條連線排隊，最長約 60 秒；輪不到回 429（帶 Retry-After，可重試，不扣點）；排隊期間不報價、不凍結點數。
- 影片：照任務排隊（queued），最長 60 分鐘；逾時 failed（upstream_busy），凍結額度全數退回。

## 目錄內比較（11 月 25 日目錄）
- DeepSeek V4 Flash 經造序，輸出每百萬 token 0.443 美元，是目錄中提供該模型的三個上游裡最低的。
- MiniMax H3 經造序，每秒 0.0068 美元起，是目錄中提供 H3 的五個上游裡起價最低的；起價依解析度與品質不同。

## MiniMax H3 產品條件（MiniMax H3 Community License，照原文列出）
- 不提供給歐盟、英國、韓國、美國的使用者。
- 不得以輸出訓練其他 AI 模型。
- 公開發布時請標示為 AI 生成。

## 來源與邊界
- AppleToken 版本歷程 API v2.65；模型目錄 GET /v2/models（2026-11-25 實讀）；AppleToken 文件。
- 單價會變動，以即時目錄為準。

人類可讀正本：https://km.idaeo.ai/post/ai/appletoken-zaoseq-upstream-20261125?utm_source=github_news&utm_medium=article&utm_campaign=zaoseq-launch&utm_content=ZSQ-github_news-zh-Hant

聯絡：appletoken@washinmura.jp

ZSQ-github_news-zh-Hant
