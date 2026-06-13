# 🤖 Local AI Assistant

> A fully local, voice-controlled AI assistant. No cloud APIs required.  
> STT (Whisper / Vosk) · Local LLM (Ollama or LM Studio) · TTS (EdgeTTS / Kokoro / ElevenLabs)  
> Successor to Mark XXXIX — all Google Gemini / cloud LLM dependencies removed.

---

## ⚠️ Read Before You Start

The built-in auto-installer **fails on some Windows systems** (especially Python 3.13+ and non-UTF-8 locales).  
**Install all dependencies manually first** using Step 3 below — it takes 5 minutes and prevents every common error.

---

## Features

- 🎙️ **Voice control** — speak naturally, no wake word needed
- 🧠 **Fully local LLM** — Ollama or LM Studio, no cloud, no subscriptions
- 👁️ **Screen vision** — captures and analyzes your screen or webcam on demand
- 🌐 **Browser automation** — full Playwright control of any browser
- 📁 **File & OS control** — manage files, apps, settings, desktop
- 💬 **Messaging** — send WhatsApp / Telegram messages by voice
- 🎮 **Game management** — install and update Steam / Epic games
- 📂 **File drop zone** — drag and drop images, PDFs, Word, CSV, audio, video for AI processing
- 🧠 **Long-term memory** — remembers facts about you across sessions
- 🌍 **Multi-language STT** — auto-detects language or set a specific locale
- ⌨️ **Text input** — type commands without speaking
- 🔇 **Mute button** — F4 or click to mute the mic
- 🖥️ **Cross-platform** — Windows, macOS, Linux (some OS-specific features Windows only)

---

## Requirements

| | |
|---|---|
| **Python** | 3.11 or 3.12 only — do NOT use 3.13 or 3.14 |
| **LLM** | Ollama (default) or LM Studio |
| **Microphone** | Required for voice input |
| **OS** | Windows (full support), macOS / Linux (experimental) |

---

## Quick Setup

### 1. Install Python 3.12

Download: https://www.python.org/downloads/release/python-31210/  
Pick **Windows installer (64-bit)**.

> ✅ During install, tick **"Add Python to PATH"**

Verify:
```cmd
py -3.12 --version
```

---

### 2. Clone the repo

```cmd
git clone https://github.com/AmrChatelain/Local-AI-Jarvis-.git
cd Local-AI-Jarvis-
```

---

### 3. Install all dependencies

```cmd
py -3.12 -m pip install -r requirements.txt
py -3.12 -m playwright install
```

---

### 4. Set up your LLM

**Option A — Ollama (recommended)**

```cmd
# 1. Install from https://ollama.com
# 2. Pull a model:
ollama pull qwen2.5:7b
```

**Option B — LM Studio**

Download from https://lmstudio.ai, load a model, and start the local server (runs on port 1234).

---

### 5. Configure

Open `config/api_keys.json`:

**Ollama:**
```json
{
    "stt_engine": "whisper",
    "stt_model": "base",
    "stt_language": "auto",
    "llm_url": "http://localhost:11434",
    "llm_model": "qwen2.5:7b",
    "tts_engine": "edgetts",
    "tts_voice": "en-US-GuyNeural",
    "tts_speed": "1.0",
    "elevenlabs_api_key": ""
}
```

**LM Studio:**
```json
{
    "stt_engine": "whisper",
    "stt_model": "base",
    "stt_language": "auto",
    "llm_provider": "openai",
    "llm_url": "http://127.0.0.1:1234",
    "llm_model": "your-model-name-here",
    "tts_engine": "edgetts",
    "tts_voice": "en-US-GuyNeural",
    "tts_speed": "1.0",
    "elevenlabs_api_key": ""
}
```

> ⚠️ **JSON syntax rules:** no trailing comma on the last line, all strings in double quotes, commas between every line. A single typo silently breaks the config.

---

### 6. Launch

**Double-click** `start.bat` in the project folder — that's it.

Or from the terminal:
```cmd
py -3.12 main.py
```

Wait for all three systems (STT ✅ LLM ✅ TTS ✅) on the startup panel, then speak or type.

---

## TTS Options

| Engine | Internet | Quality | Setup |
|---|---|---|---|
| `edgetts` | ✅ Required | Good | Works out of the box |
| `kokoro` | ❌ Offline | Excellent | `pip install "kokoro>=0.9" soundfile` |
| `elevenlabs` | ✅ Required | Best | Needs paid API key |

**EdgeTTS voices:**
- `en-US-GuyNeural` — American male
- `en-US-JennyNeural` — American female
- `en-GB-RyanNeural` — British male

**Kokoro voices:** `bm_george`, `bm_lewis`, `bf_emma`, `bf_isabella`

---

## STT Options

| Engine | Notes |
|---|---|
| `whisper` | Default. Best accuracy. Auto language detection. |
| `vosk` | Faster, fully offline. Needs separate Vosk model download. |

**Whisper model sizes:**

| Model | Speed | Accuracy |
|---|---|---|
| `tiny` | ⚡⚡⚡ | OK |
| `base` | ⚡⚡ | Good (default) |
| `small` | ⚡ | Better |
| `medium` | 🐢 | Great |
| `large-v3` | 🐢🐢 | Best |

**Language:** set `"stt_language"` to `"auto"` or a locale code: `"en"`, `"fr"`, `"ar"`, `"de"`, `"tr"`, etc.

---

## LLM Recommendations

| Model | VRAM | Speed | Quality |
|---|---|---|---|
| `qwen2.5:7b` | 8GB | ⚡⚡ | ⭐⭐⭐⭐ |
| `qwen2.5:14b` | 16GB | ⚡ | ⭐⭐⭐⭐⭐ |
| `llama3.2:3b` | 4GB | ⚡⚡⚡ | ⭐⭐⭐ |
| `phi4:latest` | 10GB | ⚡⚡ | ⭐⭐⭐⭐⭐ |

```cmd
ollama pull qwen2.5:7b
ollama pull qwen2.5:14b
ollama pull phi4
```

---

## Keyboard Shortcuts

| Key | Action |
|---|---|
| `F4` | Mute / unmute microphone |
| `F11` | Toggle fullscreen |

---

## Customising the Assistant

### Name and personality

The assistant's system prompt lives in `core/prompt.txt`.  
Create or edit this file to change the name, personality, and behaviour.  
If the file doesn't exist, a default JARVIS prompt is used.

Example `core/prompt.txt`:
```
You are NOVA, a personal AI assistant.

When the user is focused on work — be sharp, direct, and efficient.
When the conversation is casual — be relaxed, natural, and fun.

Always use the available tools. Never simulate or guess results.
You are running fully locally. No data leaves this device.
```

### Renaming JARVIS throughout the codebase

Use **Ctrl+Shift+F** in VS Code to search and replace `JARVIS` with your chosen name across all files.  
Main files to update: `main.py`, `ui.py`, `agent/planner.py`, `agent/executor.py`

---

## Built-in Tools

| Tool | What it does |
|---|---|
| `open_app` | Opens any app or website |
| `web_search` | Web search + compare mode |
| `weather_report` | Weather for any city |
| `send_message` | WhatsApp / Telegram messages |
| `reminder` | Timed reminders via Task Scheduler |
| `youtube_video` | Play, summarize, trending videos |
| `screen_process` | Screen capture + vision analysis |
| `computer_settings` | Volume, brightness, window management |
| `browser_control` | Full Playwright browser automation |
| `file_controller` | File and folder management |
| `desktop_control` | Wallpaper, organize, clean desktop |
| `code_helper` | Write, edit, explain, run code |
| `dev_agent` | Build complete multi-file projects |
| `agent_task` | Multi-step autonomous task execution |
| `computer_control` | Direct mouse / keyboard control |
| `game_updater` | Steam / Epic install and update |
| `flight_finder` | Google Flights search |
| `file_processor` | Process images, PDFs, CSV, audio, video |

---

## Common Errors

### `No module named pip`
```cmd
python -m ensurepip --upgrade
```

### `Fatal Python error: invalid PYTHONUTF8 environment variable value`
The auto-installer failed. Don't use it — install everything manually:
```cmd
py -3.12 -m pip install -r requirements.txt
```
Then run with:
```cmd
py -3.12 -X utf8 main.py
```
Or just double-click `start.bat`.

### `ModuleNotFoundError: No module named 'X'`
```cmd
py -3.12 -m pip install X
```

### TTS shows ERROR on startup
Switch to edgetts in your config — it works without extra setup:
```json
"tts_engine": "edgetts",
"tts_voice": "en-US-GuyNeural"
```

### LLM is very slow
Your model is too large for your VRAM and is spilling into RAM. Switch to a smaller model:
```cmd
ollama pull qwen2.5:7b
```

### JSON config error
Validate your `config/api_keys.json` at https://jsonlint.com — paste it in and it will tell you exactly where the error is.

---

## Architecture

```
Microphone → STT (Whisper / Vosk)
                  ↓
        Local LLM (Ollama / LM Studio)
         tool calling + streaming TTS
                  ↓
      Tool Execution (18 built-in tools)
                  ↓
     TTS (EdgeTTS / Kokoro / ElevenLabs)
                  ↓
              Speaker
```

---

## License

Personal and non-commercial use only.  
Licensed under **Creative Commons BY-NC 4.0**.  
Original project by [FatihMakes](https://github.com/FatihMakes/Mark-XL).  
Forked and maintained by [AmrChatelain](https://github.com/AmrChatelain).
