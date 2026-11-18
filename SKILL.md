---
name: cantonese-writing
description: Write authentic Hong Kong colloquial Cantonese (social posts, voice scripts, customer messages, ad copy). Use when writing any Cantonese colloquial content or preparing Cantonese TTS scripts — includes style rules, written-Chinese drift correction, few-shot bank, two-pass generation, QC rubric, and TTS pre-processing.
license: MIT
---

# Cantonese Writing Skill（廣東話口語寫作）

**核心原則：LLM 預設會 drift 返書面中文／普通話語序。呢個 skill 嘅任務係逼佢寫「香港人真係會打出嚟」嘅字。**

Companion reference：`references/lexicon.md`（60+ 書面語→口語對照 + banned Mandarin-isms）— 寫任何 output 前載入。

---

## 1. 口語 Style Rules

### 1.1 語氣助詞（用啱位，唔好堆砌）

| 助詞 | 功能 | 例 |
|---|---|---|
| 咗 | 完成體（=了） | 做咗、食咗、send 咗 |
| 緊 | 進行體（=正在） | 做緊、諗緊、傾緊 |
| 嘅 | 所有格/形容（=的） | 我嘅、好正嘅 idea |
| 啦 | 催促/建議/完結 | 快啲啦、係咁先啦 |
| 囉 | 理所當然/無奈 | 咪係囉、得囉 |
| 㗎 | 強調事實/性質 | 真㗎、好貴㗎 |
| 喎 | 轉述/提醒/意外 | 佢話得喎、幾好喎 |
| 啩 | 猜測（=吧） | 應該得啩 |
| 咩 | 反問（=嗎） | 使唔使咁誇咩 |
| 呢/嘞/喇 | 疑問尾/完成提示 | 點算呢、搞掂喇 |

**規則：**
- 一句最多 1-2 個句尾助詞；連環堆砌（「好㗎啦喎」）= 假香港人。
- 但唔好矯枉過正：日常口語句尾**應該**有語氣詞（囉/㗎/呢/喎/啦），全段句尾都冇語氣詞 = 讀落似書面語，一樣唔合格。
- 完成講「咗」唔講「了」；進行講「緊」唔講「正在」。
- 「的→嘅、是→係、不→唔、沒有→冇、他→佢、們→哋、在→喺、看→睇、說→講、給→俾、東西→嘢」— 全文一致，唔准中途變返書面。

### 1.2 書面語 drift traps（最常見出事位）

| ❌ 書面/普通話 | ✅ 口語 |
|---|---|
| 首先／然後／最後 | 第一步／跟住／最尾 |
| 其實這樣是不行的 | 其實咁樣係唔得嘅 |
| 我們需要考慮 | 我哋要諗下 |
| 非常好 | 好正／勁好 |
| 現在 | 而家 |
| 為什麼 | 點解 |
| 怎麼做 | 點做 |
| 一起 | 一齊 |
| 睡覺／起床 | 瞓覺／起身 |
| 喜歡 | 鍾意 |
| 漂亮 | 靚 |
| 便宜 | 平 |
| 累 | 攰 |
| 剛剛 | 啱啱 |
| 知道嗎？ | 知唔知？ |
| 先做X（普通話語序） | 做X先 |
| 給我看看 | 俾我睇下 |
| 多少錢 | 幾錢 |

完整表 → `references/lexicon.md`。

### 1.3 粵英 code-switching norms

香港口語自然夾英文，但**夾名詞/專業詞，唔夾動詞結構**：
- ✅ 「我哋傾下個 timeline」「幫你 handle 埋啲 admin」「個 campaign 幾時 launch？」
- ❌ 「我哋 need to 傾下」「呢個 idea is good」（英文文法骨架 = 錯）
- 動詞可借單字：check 下、send 咗、book 定、mark 低 — 但要配廣東話助詞。
- 專有名詞保留英文原樣（AI、SEO、agent、budget），唔好硬譯。
- 語氣：social post 可以夾多啲；正式 message 收斂啲，但都係口語底。

---

## 2. Few-shot Bank（bad 書面語 → good 口語）

**Pair 1 — Social post（產品）**
- ❌ 很多老闆都不知道，其實AI已經可以幫你完成大部分的行政工作。現在就開始了解吧！
- ✅ 好多老闆都唔知，其實 AI 已經幫你搞掂到大部分 admin 嘢㗎喇。仲唔快啲了解下？

**Pair 2 — Social post（抵死 tone）**
- ❌ 員工請假、辭職、要求加薪，這些問題AI員工都沒有。
- ✅ 請假？辭職？要加人工？AI 員工冇呢啲嘢囉。佢淨係識做嘢。

**Pair 3 — Voice script（開場）**
- ❌ 大家好，今天我想和大家分享三個重點。首先是關於品牌的價值。
- ✅ 哈囉大家，今日想同大家講三樣嘢。第一樣，就係品牌到底值幾錢。

**Pair 4 — Voice script（總結）**
- ❌ 總括而言，這個方案是可行的，但是需要你做一個決定。
- ✅ 簡單講，呢個方案得，但係要你拍板 — Y 定 N？

**Pair 5 — Customer message（跟進）**
- ❌ 你好，關於上次討論的項目，我們已經完成了初稿，請查收並給予意見。
- ✅ Hi 你好！上次傾嗰個 project，初稿我哋整好咗，send 咗俾你喇，得閒睇睇有咩 comment 🙏

**Pair 6 — Customer message（提醒）**
- ❌ 提醒你，付款期限是本星期五，請盡快處理。
- ✅ 提提你～今個星期五就到 payment due 喇，麻煩得閒處理埋佢啊唔該！

**Pair 7 — Ad copy（消費品）**
- ❌ 這款精華液能夠深層修護你的肌膚，現在購買可享八折優惠。
- ✅ 呢支精華勁喺渗得深，皮膚差嗰陣救命用。而家買仲有 8 折，執輸行頭慘過敗家啊。

**Pair 8 — Ad copy（B2B）**
- ❌ 聘請一位AI員工，成本只是初級員工的三分之一，而且全年無休。
- ✅ 請一個 AI 員工，使費係 junior 嘅三分一，仲要唔放假唔病唔辭職。計唔計得掂，你識㗎啦。

**Pair 9 — Social post（教育 tone）**
- ❌ 為什麼你的內容沒有人看？因為你寫的是廣告，不是內容。
- ✅ 點解你啲 content 冇人睇？因為你寫嘅係廣告，唔係內容囉。人哋一眼睇穿㗎。

**Pair 10 — Customer message（婉拒/期望管理）**
- ❌ 這個時間表比較緊迫，我們未必能夠如期完成，希望你能理解。
- ✅ 老實講個 timeline 有啲趕，我哋未必趕得切，不如傾下點樣調整好唔好？

---

## 3. 兩段式生成 Protocol（必跑）

> ⚠️ **輸出規則：Pass 1/Pass 2/rubric 全部喺內部做，只輸出最終稿。** 唔好輸出「Pass 1」「Audit」、checklist、評分表或任何前言/後記（例如「以下係回覆範本」）。

**Pass 1 — Draft**：載入 `references/lexicon.md` + 揀 2-3 條同 format/tone 匹配嘅 few-shot pair 放入 context，然後起稿。

**Pass 2 — 口語 Audit**（自我校對，checklist 逐項掃）：
1. 掃 banned list：有冇「首先/其實/然而/現在/我們/這樣/什麼/沒有/了(完成體)」等書面殘留？→ 逐個換
2. 語序：有冇普通話語序（副詞前置「先做X」）？→ 改廣東話語序（做X先）
3. 助詞：每句聽落自唔自然？有冇堆砌？完成體係咪用「咗」？
4. Code-switch：英文係咪淨係名詞/借動詞？有冇英文文法骨架滲入？
5. 讀出嚟測試：想像香港人 WhatsApp 打字 — 呢句佢會唔會咁打？唔會 → 重寫

Draft 同 Audit 之間唔准 skip。長文（>300 字）每段獨立 audit。

---

## 4. QC Rubric（5 分制，每項 1 分）

| # | 項目 | 達標條件 |
|---|---|---|
| 1 | 助詞正確 | 咗/緊/嘅/囉/㗎 等用啱位、冇堆砌、冇漏 |
| 2 | 詞彙地道 | 全文用口語詞（而家/鍾意/嘢/靚/平），零書面殘留 |
| 3 | 句式自然 | 廣東話語序，讀出嚟似真人講嘢 |
| 4 | Slang 新鮮 | 冇過時梗；tone 啱 platform |
| 5 | 無普通話 bleed | 冇「了/的/是/不/我們」滲入、冇普通話成語直搬 |

**門檻：≥4/5 先可以出街；<4 → 重跑 Pass 2。** 建議加 native speaker 抽查每批 10-20%。

---

## 5. TTS Pre-processing（粵語 TTS 通用）

1. **揀啱 voice/locale** — 例：Edge TTS `zh-HK-HiuMaanNeural`；MiniMax 類 engine 必加 language boost 參數（例 `language_boost: "Chinese,Yue"`），唔加好多 engine 會 default 讀普通話。
2. **數字**：寫中文數字或口語讀法 —「8,800」→「八千八」、「50%」→「五成」、年份可留數字，金額一律轉中文。
3. **英文詞**：常見詞（AI、app、send）讀得掂；生僻縮寫拆字母寫（「SEO」→「S E O」）；夾雜句英文前後留空格。
4. **口語字讀音**：「嘅/咗/㗎」多數粵語 TTS 讀到，但長句韻律易斷 — 句子控制喺 15-20 字內，多用標點斷句（逗號 = 停頓）。
5. **移除 emoji / markdown 符號**先 send 去 TTS。

---

## 6. Resource Budget

- 短 post（<150 字）：1 draft + 1 audit pass
- 長 script／batch：分段 audit，每 300 字一 pass
- 超過 3 次重寫仍 <4/5 → 停，交 native speaker 人手改，記低 failure pattern 更新 lexicon

---
*cantonese-writing skill · open-source edition · MIT License*
