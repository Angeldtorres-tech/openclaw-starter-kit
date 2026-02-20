# Common Errors & Solutions

Every error listed here was encountered during a real OpenClaw installation on Windows. Solutions are tested and verified.

---

## Error 1: `'iwr' is not recognized`

**Full error:**
```
'iwr' is not recognized as an internal or external command, operable program or batch file.
```

**Cause:** You're in Command Prompt (cmd.exe), not PowerShell. `iwr` (Invoke-WebRequest) is a PowerShell command.

**Fix:** Open PowerShell instead:
- Press `Win + X` → Windows PowerShell
- Or type `powershell` in your current cmd window

---

## Error 2: `running scripts is disabled on this system`

**Full error:**
```
File C:\Program Files\nodejs\npm.ps1 cannot be loaded because running scripts is disabled on this system.
```

**Cause:** Windows execution policy blocks PowerShell scripts by default.

**Fix:**
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```
Type `Y` to confirm. Then re-run your command.

---

## Error 3: `npm error syscall spawn git` / ENOENT

**Full error:**
```
npm error code ENOENT
npm error syscall spawn git
npm error path git
npm error errno -4058
```

**Cause:** Git is not installed. npm needs Git for some package operations.

**Fix:**
1. Install Git from [git-scm.com/download/win](https://git-scm.com/download/win)
2. Use all default settings in the installer
3. **Close and reopen PowerShell** (required for PATH update)
4. Re-run `npm install -g openclaw@latest`

---

## Error 4: `npm error code ENOENT` on install script

**Cause:** The install script (`iwr -useb https://openclaw.ai/install.ps1 | iex`) failed to invoke npm correctly.

**Fix:** Install directly with npm instead:
```powershell
npm install -g openclaw@latest
```

---

## Error 5: No Onboarding Wizard After Install

**Cause:** Installing via `npm install -g` (manual method) skips the interactive onboarding that the install script normally triggers.

**Fix:** Run the configuration wizard manually:
```powershell
openclaw configure
```

---

## Error 6: `gateway disconnected` in TUI

**What you see:**
```
gateway disconnected: closed | idle
```

**Cause:** The TUI is a monitoring interface — it needs the gateway to be running first.

**Fix:**
1. Press `Ctrl+C` to exit the TUI
2. Start the gateway: `openclaw gateway`
3. Then open TUI in a separate PowerShell window if needed

---

## Error 7: `Gateway start blocked: set gateway.mode`

**Full error:**
```
Gateway start blocked: set gateway.mode=local (current: unset) or pass --allow-unconfigured.
```

**Cause:** Gateway mode not configured yet.

**Fix (quick):**
```powershell
openclaw gateway --allow-unconfigured
```

**Fix (permanent):** Edit `~/.openclaw/openclaw.json` and add:
```json
"gateway": {
  "mode": "local"
}
```

---

## Error 8: `'claude' is not recognized`

**Full error:**
```
The term 'claude' is not recognized as the name of a cmdlet...
```

**Cause:** Claude Code CLI is not installed. It's needed if you want to use `claude setup-token` for Anthropic subscription authentication.

**Fix:**
```powershell
npm install -g @anthropic-ai/claude-code
```

Then run `claude setup-token`.

---

## Error 9: Daemon Needs Administrator

**What you see:**
```
Run PowerShell as Administrator or rerun without installing the daemon.
```

**Cause:** The daemon (background service) needs elevated permissions to install on Windows.

**Fix:**
1. Close PowerShell
2. Right-click PowerShell in Start menu → "Run as administrator"
3. Run `openclaw configure` → Select just "Daemon"

---

## Error 10: Skills Won't Let You Skip

**What you see:** Selecting "Skip for now" doesn't work — it says "Please select at least one option."

**Cause:** The wizard requires at least one skill to be selected.

**Fix:** Select at least one skill. Good defaults:
- `🧾 summarize` — Generally useful for any workflow
- `🐙 github` — If you use GitHub

Use spacebar to select, then Enter.

---

## Error 11: Canvas Shows "bridge missing"

**Cause:** No messaging channel is connected. The canvas test page shows bridge status.

**Fix:** Configure a messaging channel:
```powershell
openclaw configure
```
Select "Channels" → "Configure/link" → Set up Telegram (or Discord).

---

## Error 12: `npm warn deprecated` Messages During Install

**What you see:**
```
npm warn deprecated npmlog@6.0.2: This package is no longer supported.
npm warn deprecated are-we-there-yet@3.0.1: This package is no longer supported.
```

**Cause:** Some of OpenClaw's internal dependencies use older packages.

**Fix:** **Nothing to fix.** These are harmless warnings, not errors. If you see "added X packages" at the end, the installation succeeded. The deprecation warnings are for the OpenClaw maintainers to address, not you.

---

## Still Stuck?

- Run `openclaw doctor` to diagnose configuration issues
- Check logs: `%LOCALAPPDATA%\Temp\openclaw\`
- [OpenClaw Docs](https://docs.openclaw.ai/)
- [OpenClaw Discord](https://discord.gg/openclaw) (community support)
