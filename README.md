# 🎬 Subtitle Maker / 字幕メーカー

A single-file, browser-based speech-to-text tool that generates `.srt` subtitle files.  
No installation, no server, no data ever leaves your browser except to the API you choose.

ブラウザだけで動く字幕生成ツール（単一HTMLファイル）。インストール不要。音声データはあなたが選んだAPIにのみ送信されます。

---

## ✨ Features / 機能

| | EN | JA |
|---|---|---|
| Providers | OpenAI Whisper · Groq (free) · Google Gemini | OpenAI Whisper · Groq（無料枠）· Google Gemini |
| Languages | Japanese, English, Chinese, Korean, Auto-detect | 日本語・英語・中国語・韓国語・自動検出 |
| UI language | English / 日本語 toggle | EN / 日本語 切替ボタン |
| Output | Download or copy `.srt` | `.srt`のダウンロード・コピー |
| Editing | In-browser segment editing | ブラウザ上でセグメント編集 |
| Privacy | API key stays in the tab only | APIキーはタブ内のみに保持 |
| File size | Unlimited (auto-chunked for Whisper) | サイズ無制限（Whisperは自動分割） |

---

## 🚀 Usage / 使い方

### Option A — Open directly (simplest)
Double-click `subtitle-maker.html` to open it in your browser.  
> ⚠️ Some browsers block outbound `fetch` from `file://` URLs. If you get a network error, use Option B.

**最も簡単な方法:** `subtitle-maker.html`をダブルクリックしてブラウザで開く。  
> ⚠️ `file://`からのfetchをブロックするブラウザがあります。ネットワークエラーが出た場合はオプションBをお試しください。

### Option B — Local HTTP server (recommended)
```bash
# Node.js
npx serve .

# Python
python3 -m http.server 3000
```
Then open **http://localhost:3000/subtitle-maker.html**

---

## 🔑 API Keys / APIキー

### Groq (free tier / 無料)
1. Sign up at [console.groq.com](https://console.groq.com)
2. Create an API key → paste it into the tool

Model used: `whisper-large-v3`

### OpenAI Whisper
1. Get a key at [platform.openai.com/api-keys](https://platform.openai.com/api-keys)

Model used: `whisper-1`

### Google Gemini (free tier / 無料)
1. Get a free key at [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)

Model used: `gemini-2.0-flash`  
> Gemini sends the entire file in one request — no chunking needed. Best for files under ~1 hour.  
> Geminiはファイル全体を1リクエストで送信します。1時間未満のファイルに最適です。

---

## 🆚 Provider comparison / プロバイダー比較

| | Groq | OpenAI | Gemini |
|---|---|---|---|
| Cost | Free tier | Pay-per-use | Free tier |
| Speed | Very fast | Fast | Fast |
| Accuracy (JA) | ★★★★☆ | ★★★★★ | ★★★★☆ |
| Max file (per chunk) | any sizes | any sizes | any sizes |
| Chunking | 10 minutes | 10 minutes | 10 minutes |

---

## 📁 Files / ファイル構成

```
subtitle-maker.html   ← the entire app (single file)
README.md
```

---

## 🛠 How it works / 仕組み

1. **Compress** — Audio is decoded, mixed to mono, and resampled in the browser using the Web Audio API
2. **Chunk** — Large files are split into segments (Whisper providers only)
3. **Transcribe** — Each chunk is sent to your chosen API
4. **Export** — Segments are assembled into an SRT file

Gemini skips steps 1–2 and sends the raw file directly.

---

## 🔒 Privacy / プライバシー

- Your API key is stored only in the current browser tab (never in `localStorage` or cookies)
- Audio data is sent only to the API provider you select
- No analytics, no tracking, no third-party scripts

---

## 📄 License

MIT — free to use, modify, and distribute.
