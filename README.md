# cantonese-writing 🇭🇰

**令你個 AI agent 覆客似香港人。**
*Hong Kong Cantonese for customer-facing agents. MIT, commercial use OK.*

你叫 AI 用廣東話覆客，十次有九次出書面語 —「您好」「我們」「非常抱歉」，溝兩粒「嘅」就當交貨。香港人一眼睇穿。呢個 skill 令任何 LLM 講返地道港式口語：唔使 fine-tune、唔使 GPU、$0。

## Install

```bash
npx skills add [GITHUB-URL-待補] --skill cantonese-writing
```

任何 agent framework（Claude Code / OpenClaw 等）即用。MIT license，商業用途 OK。

## Before / After（真實輸出，base vs +skill，一字冇改）

**退款要求：**
> ❌ 您好，感謝您聯絡。根據我哋嘅退換政策，產品係唔設退款嘅。如果您想了解多啲細節…（官腔 + 自己解釋政策）
> ✅ 客人你好，唔好意思聽到你咁唔開心😔 退款嘅事我會幫你轉同事親自跟進，麻煩你俾返姓名同聯絡電話…（人味 + 正確升級真人）

**傳媒查詢：**
> ❌ 您好！多謝您嘅查詢。您可以…或者您都可以留低您嘅姓名…（五個「您」）
> ✅ 你好！多謝你對我哋嘅關注～呢啲資料我唔可以即刻答你，麻煩你留低姓名同電話，同事會親自聯絡你傾詳情啊！

（完整對照 + 第三組：`docs/before-after.md`）

## 入面有乜

- **88 行書面語→口語 lexicon**（您好→你好、我們→我哋、非常抱歉→真係唔好意思…）
- **普通話用語 banned list**（視頻/質量/立馬，見到即改）
- **兩段式生成 + 自我 audit**：起草 → 對 checklist 自檢 → 出稿（checklist 唔會外洩俾客睇）
- **TTS 稿前處理規則**：數字讀法、品牌名逐字母、短句化（連住 zh-HK 語音先自然）
- **CS overlay 範本**（experimental）：事實閘（冇數據就問，唔老作）、四種情況先轉真人、醫療零承諾

## Evidence

- Cross-family 盲評（AI 評審唔評自己廠）：寫作 skill vs base 最高 20:0；CS 場景全五項 clean 由 38/54 → 47/54（+ overlay 規則）
- 真人盲測：[進行中 — 結果出咗即刻貼]
- 已用於香港美容品牌 WhatsApp/IG 客服生產線

## 你應該用邊個？

| 你想要 | 用 |
|---|---|
| 連登體 / 創作粵文 | [tzengyuxio/written-cantonese](https://github.com/tzengyuxio/skills)（非商用 license） |
| 短片口播稿去 AI 味 | garrickbuilds/speak-human-hk |
| 自己 host 粵語 model | [hon9kon9ize](https://github.com/hon9kon9ize) |
| **商用 agent 覆客講港話** | **呢個** |

## Limitations（老實講）

- 真人盲測樣本量：待補
- STT（SenseVoice/whisper）同 TTS（edge-tts）模組屬 experimental
- lexicon 香港口語會過時 — 歡迎 PR 加詞

MIT License. Cantonese is spoken by ~85M people and chronically underserved in AI — help fix that.
