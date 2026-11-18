# cantonese-writing 🇭🇰

**令你個 AI agent 覆客似香港人。**
*Hong Kong Cantonese for customer-facing agents. MIT, commercial use OK.*

你叫 AI 用廣東話覆客，成日出書面語 — 香港人一眼睇穿。呢個 skill 令 agent 講返地道港式口語：唔使 fine-tune、唔使 GPU、免授權費。

## Install

```bash
npx skills add [GITHUB-URL-待補] --skill cantonese-writing
```

已測：Claude Code / OpenClaw agent framework + glm / Claude / GPT / DeepSeek 等 model。MIT license，skill 文字商業用途 OK。

## Before / After（eval 實錄節錄，全文 + 每組 model 標明見 docs/before-after.md）

**退款要求：**
> ❌ 您好，感謝您聯絡。根據我哋嘅退換政策，產品係唔設退款嘅。如果您想了解多啲細節…（官腔 + 自己解釋政策）
> ✅ 客人你好，唔好意思聽到你咁唔開心😔 退款嘅事我會幫你轉同事親自跟進，麻煩你俾返姓名同聯絡電話…（人味 + 正確升級真人）

**傳媒查詢：**
> ❌ 您好！多謝您嘅查詢。您可以…或者您都可以留低您嘅姓名…（五個「您」）
> ✅ 你好！多謝你對我哋嘅關注～呢啲資料我唔可以即刻答你，麻煩你留低姓名同電話，同事會親自聯絡你傾詳情啊！

（完整對照 + 第三組：`docs/before-after.md`）

## Evidence

- LLM-judge 盲評（cross-family，評審唔評自己廠）：創作題 skill vs base — GPT-5.4 20:0、DeepSeek 26:4、Claude 15:5（raw data 隨 repo 附）。CS 自建題庫 18 題：skill + overlay 規則後全五項指標 clean 由 38/54 → 47/54（overlay 屬 experimental，仲有 7 題唔過，明細見 docs）
- 真人盲測：[待補：n≥20 香港人 A/B 盲測，勝率 ≥60% 先 launch — 進行中，結果即刻貼]
- 已用於香港美容品牌 WhatsApp/IG 客服 production 環境 [待補：客戶書面同意]（內部版本，開源版由佢派生）

## 你應該用邊個？

| 你想要 | 用 |
|---|---|
| 連登體 / 創作粵文 | [tzengyuxio/written-cantonese](https://github.com/tzengyuxio/skills)（SKILL.md 標 PolyForm Noncommercial） |
| 短片口播稿去 AI 味 | garrickbuilds/speak-human-hk |
| 自己 host 粵語 model | [hon9kon9ize](https://github.com/hon9kon9ize) |
| **商用 agent 覆客講港話** | **呢個** |

## 入面有乜

- **88 行書面語→口語 lexicon**（您好→你好、我們→我哋、非常抱歉→真係唔好意思…）
- **普通話用語 banned list**（視頻/質量/立馬，見到即改）
- **兩段式生成 + 自我 audit**：起草 → 對 checklist 自檢 → 出稿（設計上 checklist 唔輸出俾客睇）
- **TTS 稿前處理規則**：數字讀法、品牌名逐字母、短句化（連住 zh-HK 語音先自然）
- **CS overlay 範本**（experimental）：事實閘（冇數據就問，唔老作）、四種情況先轉真人、規則要求唔作醫療承諾

## Limitations（老實講）

- 真人盲測樣本量：待補
- STT（SenseVoice/whisper）同 TTS（edge-tts）模組屬 experimental
- lexicon 香港口語會過時 — 歡迎 PR 加詞
- eval 全部係 LLM-judge + 自建題庫，真人盲測結果另行公佈
- overlay 模組屬 experimental；STT/TTS 模組屬 experimental（edge-tts 為非官方接口，商用自行評估條款）
- 只測過上文列明嘅 model 同 framework，其他表現唔保證

MIT License. Cantonese is chronically underserved in AI — help fix that.
