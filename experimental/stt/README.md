# Module 01 — STT（聽 / Listen）

WhatsApp 語音（OGG/Opus）→ 廣東話文字。本地離線，零 API 費用。

## 點解用呢個組合

| 組件 | 選擇 | 理由 |
|---|---|---|
| Engine | faster-whisper (CT2) | CPU 上 int8 量化已夠快，唔使 GPU |
| Model | `whisper-small-cantonese-ct2` | 廣東話 fine-tune；實測轉錄準確度極高（口語语气助詞都執到） |
| 成本 | $0 | 完全本地，冇 API call |

## 安裝

```bash
pip install faster-whisper
```

Model 下載（Hugging Face CT2 format）：

```bash
# 揀一個位置放 model，例如 repo 旁邊
mkdir -p models
# 用 huggingface-cli（pip install huggingface_hub 如未有）
huggingface-cli download JackyHoCL/whisper-small-cantonese-yue-english-ct2 \
  --local-dir models/whisper-small-cantonese-ct2
```

> 要嘅係 CT2 conversion 版本（目錄入面有 `model.bin` + `config.json`
> + `vocabulary.json`）。上面 repo 已核實齊三件；本地目錄名簡化做
> `whisper-small-cantonese-ct2` 冇問題，faster-whisper 只睇內容。

## 用法

```bash
python3 stt.py voice.ogg
# → 印出廣東話轉錄文字
```

Model 位置三揀一（唔使改 code）：

1. `--model-dir /path/to/model` flag
2. `CANTO_STT_MODEL_DIR` env var
3. 預設 `./models/whisper-small-cantonese-ct2`（相對 cwd）

## Known Issue（必讀）

**語言保持 AUTO，唔好 force `yue`。**

呢個 Cantonese fine-tune model 喺 auto 模式先至正確輸出廣東話；
強制 `--lang yue` 會輸出**空字串**。實測復現過，唔係玄學。
只有轉非粵語內容先至需要 `--lang`（例如 `--lang zh`）。

## 依賴

- Python 3.10+
- `faster-whisper`（會自動帶 ctranslate2）
- ffmpeg 喺 PATH（faster-whisper decode OGG/Opus 要）

## 上游

模組源自生產環境 WA voice-reply pipeline（Phase 1，round-trip 已實證），
round-trip 實證見 `../../evals/R4_voice_roundtrip/`。
