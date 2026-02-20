# OpenClaw Windows Install Guide

A detailed walkthrough for installing and configuring OpenClaw on Windows 10/11.

---

## Step 0: Use PowerShell, Not CMD

**This is the #1 mistake.** OpenClaw's install script uses PowerShell commands. If you see `'iwr' is not recognized`, you're in Command Prompt.

**How to open PowerShell:**
- Press `Win + X` → Select "Windows PowerShell" or "Terminal"
- Or: Start menu → type "PowerShell" → click it
- Or: In any cmd window, type `powershell` and press Enter

---

## Step 1: Set Execution Policy

Windows blocks scripts by default. Fix this once:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Type `Y` when prompted. This allows locally-created scripts and signed remote scripts to run.

**If you want temporary access only** (resets when you close PowerShell):
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

---

## Step 2: Install Git

npm needs Git for some packages. Without it, you'll get `spawn git ENOENT` errors.

1. Download from [git-scm.com/download/win](https://git-scm.com/download/win)
2. Run the installer — **use all default settings** (just click Next through everything)
3. **Close and reopen PowerShell** after installing (so PATH updates)

Verify:
```powershell
git --version
```

---

## Step 3: Install Node.js

If you don't already have it:

1. Download LTS from [nodejs.org](https://nodejs.org/)
2. Run installer — check the box "Automatically install necessary tools"
3. Restart PowerShell

Verify:
```powershell
node --version
npm --version
```

---

## Step 4: Install OpenClaw

**Option A: Direct npm install (recommended)**
```powershell
npm install -g openclaw@latest
```

**Option B: Install script**
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

You'll see some `npm warn deprecated` messages — these are harmless. As long as it says "added X packages," you're good.

---

## Step 5: Initial Setup

```powershell
openclaw setup
```

This creates the config files and workspace directory.

---

## Step 6: Configure

```powershell
openclaw configure
```

This launches an interactive wizard. Select all sections:
- ✅ Workspace
- ✅ Model
- ✅ Web tools
- ✅ Gateway
- ✅ Channels
- ✅ Skills
- ✅ Health check

Use arrow keys to navigate, spacebar to select, Enter to confirm.

### Key Configuration Steps

**Model Setup:**
- If you have an Anthropic subscription (Pro/Max): Choose "Anthropic token" → Install Claude Code (`npm install -g @anthropic-ai/claude-code`) → Run `claude setup-token` → Copy token to Notepad first (ensure one line, no breaks) → Paste into configure
- If you have an API key: Choose "Anthropic API key" → Paste your key from console.anthropic.com

**Web Tools:**
- Enable Brave Search → Get free API key from [brave.com/search/api](https://brave.com/search/api)

**Gateway:**
- Port: 18789 (default)
- Bind mode: Loopback (local only)
- Auth: Token (recommended)
- Tailscale: Off

**Channels (Telegram):**
1. Open Telegram → Search `@BotFather`
2. Send `/newbot`
3. Choose a name and username (must end in `bot`)
4. Copy the bot token BotFather gives you
5. Paste into the configure wizard

**Daemon:**
- Requires Administrator. Right-click PowerShell → "Run as administrator" → Run `openclaw configure` → Select just Daemon

**Skills:**
- Select at least one (e.g., `summarize`) — the wizard requires a selection

---

## Step 7: Start the Gateway

```powershell
openclaw gateway
```

If you get `Gateway start blocked`, use:
```powershell
openclaw gateway --allow-unconfigured
```

You should see:
```
[gateway] listening on ws://127.0.0.1:18789
```

**Don't close this PowerShell window** — it keeps the gateway running.

---

## Step 8: Connect

Open Telegram → Find your bot → Send a message. Your OpenClaw should respond!

Or open the canvas in a browser:
```
http://127.0.0.1:18789/__openclaw__/canvas/
```

---

## Step 9: Customize Your Workspace

Copy the templates from this repo into `~/.openclaw/workspace/`:
- `AGENTS.md` — How your agent behaves
- `SOUL.md` — Agent personality
- `USER.md` — Tell it about yourself
- `HEARTBEAT.md` — Periodic tasks

---

## Troubleshooting

See [Common Errors Guide](common-errors.md) for detailed solutions to the 12 most common issues.
