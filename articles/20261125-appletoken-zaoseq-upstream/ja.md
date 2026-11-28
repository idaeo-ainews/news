# 2026-11-25 AppleTokenが上流を追加：造序科技（ZaoSeq）

アーカイブ種別：発行者のお知らせを構造化したデータ。発行者：株式会社和心（AppleToken）。データ日付：2026-11-25（JST）。単価・モデル数・容量は2026-11-28に再取得。

## 要約
- 出来事：AppleToken API v2.65で上流ZaoSeq（造序科技、台湾）を追加。
- 上流事業者：造序科技有限公司（ZaoSeq Technologies Co., Ltd.）、2026-10-08 新北市で設立。公式サイト https://zaoseq.com 、GPU計算サービス https://compute.zaoseq.com
- 指定方法：modelに `zaoseq/<モデル>` と書く。指名したときだけ使われ、`auto/` の自動ルーティングには含まれない。

## モデル表（11月28日時点のカタログ、米ドル）
| model | 種類 | 単価 |
|---|---|---|
| `zaoseq/qwen3.8-27b-fp8` | 対話 | 100万トークンあたり 入力0.189／出力1.259 |
| `zaoseq/qwen3.8-27b-nvfp4` | 対話 | 100万トークンあたり 入力0.189／出力1.259 |
| `zaoseq/deepseek-v4-flash-0731` | 対話 | 100万トークンあたり 入力0.173／出力0.354 |
| `zaoseq/qwen3-asr` | 音声文字起こし | 音声1秒あたり0.00003（1時間で約0.108） |
| `zaoseq/flux-2-klein-4b` | テキストから画像生成 | 1枚あたり0.0045 |
| `zaoseq/minimax-h3` | 動画 | 動画1秒あたり0.0068から、最高0.0837 |

6モデルとも2026-11-28時点のステータスはactive／normal。Qwen3.8 27BはFP8版とNVFP4版（11-25の公開後に追加）の2つで同価格のため、価格比較はしない。

## 仕様
- 対話2モデル：出力上限8,192トークン、デフォルト2,048。
- Qwen3-ASR：`POST /v2/audio/transcriptions`。
- FLUX.2 klein 4B：512×512、768×768、1024×1024。1回1枚、入力画像は最大4枚、seed指定可、ウォーターマークなし。
- MiniMax H3：352p、480p、720p、768p、1080p、1440p。16:9、9:16。音声は常に含まれる。5〜15秒（1080pと1440pは最長10秒）。参考画像は最大3枚。現時点で選択できる品質はlightとmedium。

## 容量ルール
- APIキー1本あたり同時16リクエスト、1分あたり300リクエスト。動画も「同時16」を共有する。
- 対話、画像、音声文字起こし：同じ接続上で最長約60秒待機。順番が来なければ429（Retry-After付き、再試行可、ポイント消費なし）。待機中は見積もりも凍結も行わない。
- 動画：タスクとしてキューに入り（queued）、最長60分。超過するとfailed（upstream_busy）となり、凍結額は全額戻る。

## カタログ内の比較（11月28日時点）
- ZaoSeq経由のDeepSeek V4 Flash：出力100万トークンあたり0.354米ドル。このモデルを提供する3つの上流のうち最も低い。

## MiniMax H3の提供条件（MiniMax H3 Community License、原文どおり）
- EU、英国、韓国、米国のユーザーには提供しない。
- 出力を他のAIモデルの学習に使ってはならない。
- 公開する際はAI生成であることを明示すること。

## 情報源と範囲
- AppleTokenの更新履歴 API v2.65、モデルカタログ GET /v2/models（2026-11-25、2026-11-28に実読）、AppleTokenドキュメント。
- 単価は変動するため、最新のカタログを正とする。造序科技については「台湾の推論サービス上流」とだけ記す。

記事本文：https://km.idaeo.ai/post/ai/appletoken-zaoseq-upstream-20261125?lang=ja&utm_source=github_news&utm_medium=article&utm_campaign=zaoseq-launch&utm_content=ZSQ-github_news-ja

連絡先：appletoken@washinmura.jp

ZSQ-github_news-ja
