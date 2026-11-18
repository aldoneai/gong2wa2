# Module 04 — TTS（講 / Speak）

廣東話文字 → OGG/Opus 語音（WhatsApp voice note 格式）。用微軟 edge-tts 粵語聲，零費用。

## 點解用呢個組合

| 組件 | 選擇 | 理由 |
|---|---|---|
| Engine | edge-tts（Microsoft Edge 線上語音） | $0、粵語聲質素好、唔使自己養模型 |
| Voice | `zh-HK-HiuMaanNeural` | 女聲自然，CS/通知類場景實測可用 |
| 輸出 | OGG/Opus 32k 48kHz | WhatsApp voice note 原生格式 |

## 安裝

```bash
pip install edge-tts
# ffmpeg 要喺 PATH（mp3 → ogg/opus 轉碼用）
sudo apt install ffmpeg   # Debian/Ubuntu
```

## 用法

```bash
python3 tts.py "你張訂單已經出咗貨喇，兩三日內送到。"
# → 印出 .ogg 輸出路徑

echo "段稿" | python3 tts.py -          # stdin都得
python3 tts.py "段稿" --out reply.ogg    # 自訂輸出位置
python3 tts.py "段稿" --voice zh-HK-WanLungNeural   # 揀男聲
```

Env vars（可選）：
- `CANTO_TTS_VOICE` — 預設聲線
- `CANTO_TTS_TMPDIR` — 中間檔/預設輸出目錄

## 朗讀稿規則（重要）

TTS 讀出嚟好唔好聽，七成決定喺**稿**，唔係聲線。落 TTS 前照
`../../core/cantonese-writing/references/tts.md` 執稿：
- 數字轉中文讀法（四百四十八，唔係 448）
- 短句、正常標點；零省略號、零括號拼音提示
- 品牌名逐字拆寫

## 依賴

- Python 3.10+（asyncio）
- `edge-tts`、`ffmpeg`

## 上游

源自生產環境 WA voice-reply pipeline（Phase 1，round-trip 已實證），
round-trip 實證見 `../../evals/R4_voice_roundtrip/`。
