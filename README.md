# glass

A floating AI copilot that sits on top of your screen — sees what you see, hears your meetings, and answers in real time. Bring your own API key (OpenAI, Anthropic, or Google Gemini).

Built on Electron. No server, no account, no telemetry — your key and your data stay on your machine.

> **Heads up:** the "stay hidden from screen shares" trick relies on a macOS-only window flag. On Windows, glass runs great but is visible in screen shares like any normal window.

---

## Features

| Feature | What it does |
|---|---|
| **Assist** (`Ctrl+Enter`) | Looks at your screen + recent conversation, tells you the next move |
| **What should I say?** | Listens to your mic + the other person's audio, suggests a reply |
| **Follow-up questions** | Generates questions based on the conversation so far |
| **Recap** | Summarizes the whole conversation |
| **Solve a coding problem** (`Ctrl+H`) | Screenshots a coding problem, returns a solution with time/space complexity |
| **New Chat** (`Ctrl+Shift+N`) | Clears the panel and resets the transcript/history |
| **Smart toggle** | Switch between a fast/cheap model and a slower/smarter one |

---

## Quickstart (Windows)

Open PowerShell and paste this whole block:

```powershell
# 1. Clone the repo
git clone https://github.com/P-r-e-m-i-u-m/glass-.git
cd glass-

# 2. Install dependencies
npm install

# 3. Launch
npm start
```

Requires [Node.js 18+](https://nodejs.org) — install that first if `npm` isn't recognized.

### One-click launch (optional)
Instead of reopening a terminal every time, create a desktop shortcut that launches glass in one click:

```powershell
$appFolder = "$PWD"
$desktopPath = [Environment]::GetFolderPath("Desktop")

@"
@echo off
cd /d "$appFolder"
npm start
"@ | Set-Content -Path "$appFolder\start-glass.bat" -Encoding ASCII

$WshShell = New-Object -ComObject WScript.Shell
$Shortcut = $WshShell.CreateShortcut("$desktopPath\glass.lnk")
$Shortcut.TargetPath = "$appFolder\start-glass.bat"
$Shortcut.WorkingDirectory = $appFolder
$Shortcut.Save()

Write-Host "Shortcut created on your Desktop."
```

---

## Setting up your API key

1. Launch glass, click the **⚙ Settings** icon (bottom-right of the composer).
2. Pick a provider and paste your key:
   - **OpenAI** — [platform.openai.com/api-keys](https://platform.openai.com/api-keys) (chat + Whisper transcription, paid)
   - **Anthropic (Claude)** — great for reasoning/coding, but has no speech-to-text of its own; pair it with an OpenAI or Gemini key if you want the listening features
   - **Google Gemini** — [aistudio.google.com/apikey](https://aistudio.google.com/apikey) (free tier available, handles both chat *and* transcription with a single key — recommended if you want the whole thing free)
3. Set your **fast** and **smart** model names for that provider (e.g. `gemini-2.5-flash` / `gemini-2.5-pro`).
4. Close Settings — you're ready to go.

One key covers everything for that provider. It's stored only in a local `cue-data.json` config file and sent only to that provider.

---

## Listening on a call

1. Click the **listen** button in the toolbar (green dot = live).
2. When the audio-share picker appears, choose **Entire Screen** and make sure **share system audio** is checked — otherwise glass only hears your mic, not the other person.
3. Ask **"What should I say?"** any time during the call, or **Recap** afterward.

---

## Troubleshooting

**`404 Not Found` on a model call**
The model name is outdated/deprecated. Open Settings, update the fast/smart model string to a current one (e.g. `gemini-2.5-flash` instead of `gemini-1.5-flash`).

**`429 Too Many Requests`**
You've hit your provider's free-tier rate limit. Switch off "Smart" mode (heavier models have much smaller free quotas), wait a bit, or add billing to your key.

**Listening does nothing / empty transcript**
Make sure you picked "Entire Screen" (not a single window) and ticked "share system audio" in the picker — Windows only exposes system-audio loopback that way.

**Responses are slow**
Turn off "Smart" mode, or switch your fast model to a lighter one (e.g. `gemini-2.5-flash-lite`).

---

## Disclaimer

glass is built for legitimate uses — personal notes, studying, accessibility, and practice. Using a hidden or AI-assisted overlay during a proctored exam, job interview, or recorded meeting may violate that platform's rules and, depending on where you are, consent laws. You're responsible for how you use it.

## License

GPL-3.0-or-later — see [LICENSE](LICENSE).
