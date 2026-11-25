# Local Voice AI Stack: SillyTavern + AllTalk TTS V2 + Ollama/KoboldCpp/LM Studio + Faster-Whisper

**Fully offline, private, real-time voice chat** with custom character voices (e.g. Arkham-style Joker or Batman), emotion expression, long-term memory, and reasoning.

This repository is a complete, ready-to-follow guide and starter project for building a high-quality local AI voice companion / roleplay system.

## Features

- **100% local / offline** after initial model downloads
- Real-time microphone input (Faster-Whisper) + speaker output
- **Voice cloning** via AllTalk TTS V2 (XTTS-v2, F5-TTS, RVC, etc.)
- Custom character voices from short audio samples (Joker laugh, Batman tone, etc.)
- Emotion & expressive speech (exaggeration, style controls, prompt-driven laughs/tone shifts)
- Strong memory + reasoning via SillyTavern character cards + local LLM
- Autonomous chatting with consistent personality
- Multi-character support and narrator voices

## Recommended Hardware

- NVIDIA GPU with **8 GB+ VRAM** (12–16 GB ideal for comfortable cloning + larger models)
- 16 GB+ system RAM
- Windows 10/11 or Linux (Ubuntu recommended)
- Fast SSD

CPU-only is possible with lighter models but will be slower.

## Core Components

| Component              | Role                              | Official Source / Notes                                      |
|------------------------|-----------------------------------|--------------------------------------------------------------|
| **SillyTavern**        | Frontend, characters, memory, TTS | https://github.com/SillyTavern/SillyTavern                   |
| **AllTalk TTS V2**     | Local TTS + voice cloning         | https://github.com/erew123/alltalk_tts (branch `alltalkbeta`) |
| **Ollama** (or LM Studio / KoboldCpp) | Local LLM (reasoning + memory) | https://ollama.com                                           |
| **Faster-Whisper**     | Speech-to-Text (microphone)       | https://github.com/SYSTRAN/faster-whisper                    |

## Quick Start Overview

1. Install **Ollama** (or LM Studio / KoboldCpp) and pull a model (e.g. `qwen2.5:14b`, `llama3.1:8b`, or larger).
2. Install **SillyTavern** (official launcher recommended).
3. Install **AllTalk TTS V2** (standalone recommended).
4. Install **Faster-Whisper** (or use a SillyTavern STT extension / Whisper.cpp).
5. Connect everything inside SillyTavern:
   - API → Ollama / Text Completion
   - TTS → AllTalk (endpoint usually `http://127.0.0.1:7851`)
   - STT → your Whisper setup
6. Create / import character cards and assign cloned voices.
7. (Optional) Prepare clean 5–30 second voice samples of your target characters and clone them in AllTalk.

Detailed step-by-step instructions are in the sections below and in the `docs/` folder.

## 1. Install Local LLM (Ollama – Recommended)

```bash
# Windows / macOS: download from https://ollama.com
# Linux:
curl -fsSL https://ollama.com/install.sh | sh

# Pull a good model for roleplay + reasoning
ollama pull qwen2.5:14b          # excellent balance
# or
ollama pull llama3.1:8b
ollama pull gemma2:27b           # if you have enough VRAM
```

Keep Ollama running. Default API: `http://127.0.0.1:11434`

Alternatives:
- **LM Studio** – GUI, easy model management
- **KoboldCpp** – very popular with SillyTavern users

## 2. Install SillyTavern

Official way (recommended):

- Use the **SillyTavern Launcher**: https://github.com/SillyTavern/SillyTavern-Launcher

Or clone manually:

```bash
git clone https://github.com/SillyTavern/SillyTavern
cd SillyTavern
npm install
node server.js
```

Open `http://127.0.0.1:8000` (or the port shown).

## 3. Install AllTalk TTS V2 (Voice Cloning)

**Recommended branch:** `alltalkbeta`

```bash
git clone -b alltalkbeta https://github.com/erew123/alltalk_tts
cd alltalk_tts

# Windows
atsetup.bat

# Linux
chmod +x atsetup.sh
./atsetup.sh
```

Follow the interactive prompts (Standalone installation is best for most users).

After installation, start AllTalk:

```bash
# Windows
start_alltalk.bat

# Linux
./start_alltalk.sh
```

Default API / web UI: `http://127.0.0.1:7851`

### Voice Cloning Tips (Joker / Batman style)

1. Extract **clean** short clips (5–30 seconds) of clear dialogue from the games (minimal music/SFX).
2. Place the `.wav` files in AllTalk’s speakers / voices folder.
3. Use **XTTS** or **F5-TTS** engine + optional **RVC** for higher fidelity.
4. In SillyTavern → TTS → AllTalk → map the cloned voice to your character.
5. For emotion (Joker laugh, manic tone):
   - Use strong system prompts / character cards that encourage expressive language.
   - Experiment with AllTalk engine settings (speed, temperature, exaggeration where available).

**Legal note:** Only use voice samples you have the right to use. Keep everything private and non-commercial.

## 4. Speech-to-Text (Faster-Whisper)

Install Faster-Whisper:

```bash
pip install faster-whisper
```

You can run a simple local server or use community SillyTavern STT extensions that support Whisper / Faster-Whisper.

Popular options:
- Direct microphone → Faster-Whisper → paste into SillyTavern
- Dedicated STT extensions / bridges available in the SillyTavern community

For continuous / push-to-talk experience, many users combine it with Silero VAD.

## 5. Connect Everything in SillyTavern

1. **API Connections**
   - Choose Ollama (or Text Completion + your backend)
   - URL: `http://127.0.0.1:11434`
   - Select your model

2. **TTS Extension**
   - Provider: **AllTalk**
   - Endpoint: `http://127.0.0.1:7851` (confirm in AllTalk console)
   - Enable + Auto Generation
   - Create Voice Map: assign cloned voices to characters and narrator

3. **STT**
   - Configure your Faster-Whisper setup or extension

4. **Character Card**
   - Create a strong system prompt / character definition for Joker, Batman, or any persona
   - Include memory instructions and emotional style guidelines

## Project Structure (this repo)

```
local-voice-ai-sillytavern-alltalk/
├── README.md                 # This file
├── docs/
│   ├── setup-windows.md
│   ├── setup-linux.md
│   ├── voice-cloning-guide.md
│   └── character-examples/
├── characters/               # Example SillyTavern character cards (JSON)
├── voices/                   # Placeholder for your reference audio samples
├── scripts/                  # Helper scripts (start services, etc.)
└── LICENSE
```

## Example Character Ideas

- **Arkham Joker** – chaotic, manic, frequent laughs, unpredictable reasoning
- **Bruce Wayne / Batman** – deep, controlled, logical, dry humor
- Custom companions with long-term memory and autonomous behavior

Place clean reference audio in `voices/` and clone them inside AllTalk.

## Troubleshooting

- **AllTalk not appearing in SillyTavern** → Make sure AllTalk is running first, then reload the TTS extension page.
- **Low quality clone** → Use cleaner, longer, higher-quality reference samples. Try RVC.
- **High latency** → Use smaller LLM + faster TTS engine (or enable DeepSpeed / Low VRAM mode in AllTalk).
- **CUDA / GPU issues** → Check NVIDIA drivers and that AllTalk / Whisper are using the GPU.

## Useful Links

- SillyTavern: https://github.com/SillyTavern/SillyTavern
- AllTalk TTS V2: https://github.com/erew123/alltalk_tts (use `alltalkbeta` branch)
- AllTalk Wiki: https://github.com/erew123/alltalk_tts/wiki
- Ollama: https://ollama.com
- Faster-Whisper: https://github.com/SYSTRAN/faster-whisper
- SillyTavern Docs (TTS): https://docs.sillytavern.app/extensions/tts/

## License

This guide and repository structure are provided under MIT License.  
Individual components (SillyTavern, AllTalk, models, etc.) retain their original licenses.

---

**Enjoy your private, offline, expressive AI voice companion.**  
Feel free to open issues or PRs with improvements, character cards, or helper scripts.
