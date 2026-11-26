# Agent Sentinel

Version: 0.1.0 · MIT License

On-demand security awareness for coding agents. No background process, server, telemetry or automatic reports. The installer registers a short trigger in user-level instructions and copies a local `SKILL.md`. Read the scripts before running them; no administrator permissions or network access are required.

## Install / 安裝

From this directory, run the appropriate local shell script. By default it installs for detected Claude Code, Codex and OpenCode clients (a CLI or its config directory exists). It does not change project files.

macOS / Linux / Git Bash:

```sh
bash install.sh
# Or explicitly select a client:
bash install.sh claude
```

Windows PowerShell:

```powershell
.\install.ps1
# Or explicitly select a client:
.\install.ps1 -Client claude
```

Other explicit choices: `codex`, `opencode`, `all`. If PowerShell policy prevents execution, inspect the script and use an approved environment (e.g. Git Bash); do not disable security controls. Restart the affected agent sessions after installation. To verify, ask the agent where the Sentinel skill is stored and when it loads it, without running suspicious commands.

The installer appends one marked block without replacing existing instructions, backs up existing files before modification, and skips duplicate registration. Claude and Codex custom home environment variables and OpenCode XDG_CONFIG_HOME are supported. If Codex has AGENTS.override.md, registration uses that active file. Nonstandard client setups may require manual configuration. If switching Codex override files later, rerun for the active configuration.

## Update / 更新

Get the latest release or pull the repository, then rerun the same installer. It refreshes the local SKILL.md and backs up a changed copy. Existing trigger text is not overwritten. If a future release changes the trigger, remove only the marked block described below and rerun the installer. Restart agent sessions. Use the same shell family as the original installation to avoid path-format differences.

## Uninstall / 移除

Remove only the block between `<!-- agent-sentinel:begin -->` and `<!-- agent-sentinel:end -->` (inclusive) from each registered instruction file, and remove the corresponding `agent-sentinel/SKILL.md` if no longer needed. Installer output shows exact paths and backups. Do not delete the whole instructions file or shared skills directory. No automatic removal of other files.

## How it works

Only suspicious observations trigger a local skill read, safe verification and optional user-reviewed reporting draft. Normal work continues without additional scans. This is advisory, not a security boundary. The agent may miss threats or misclassify content; verify with independent evidence. No automatic submissions.

## Reporting and compatibility

Microsoft SmartScreen handles suspicious websites across platforms; Defender submissions are mainly for Microsoft-related detections and false positives. For other services, use the relevant provider's official channel. Bash installer tested with isolated HOME directories; PowerShell is provided but has not been tested on Windows. No cross-model detection benchmark yet.

## 中文

安裝後自動加入全域 CLAUDE.md 或 AGENTS.md，平常只保留簡短觸發提醒，遇到可疑網頁、指令或防毒警告才讀取本機 SKILL.md。使用者決定是否通報，不自動上傳。重複安裝不重複註冊，原有指令保留並備份。
