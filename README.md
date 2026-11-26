# Agent Sentinel

Version: 0.1.0 · MIT License

> Every agent can be a sentinel.

A lightweight, on-demand security SOP for coding agents, created in response to ClickFix-style attacks that trick people or agents into executing untrusted instructions.

**Pause. Verify. Report when warranted.**

## Design philosophy

Agent Sentinel is a deliberately small project. It gives agents a practical procedure for recognizing suspicious instructions, investigating them safely, and helping users prepare a responsible disclosure report.

- **Token discipline.** Avoid repetitive checks and unnecessary API consumption. Keep only a short trigger in persistent instructions; load the full skill when suspicious behavior is encountered.
- **Minimal footprint.** No runtime scripts, background scans, additional dependencies, server, telemetry or automatic reports. The installer only registers the trigger and copies a local Markdown file. Inspect the local installer before running it; no administrator permissions or network access are required.
- **Agent autonomy.** As models improve, they may become better at applying the same SOP. Prefer contextual reasoning over an ever-growing collection of hard-coded detection rules.
- **Responsible disclosure.** Make it easier to do the right thing. Pause the suspicious action, verify the evidence, continue unrelated work, and offer a reporting draft when justified. The user decides whether to submit it.

Agent Sentinel is designed to complement sandboxing and existing security controls, not replace them. It is a measured response to social engineering: reduce the friction of reporting without creating unnecessary friction in everyday development.

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

Agent Sentinel 源於對 ClickFix 類誘導執行攻擊的思考。開發者不應為了資安而被迫消耗大量 API 額度、執行額外程序或安裝不必要的依賴。與其不斷擴張偵測規則，不如給 Agent 一套簡潔的「停、查、報」SOP，運用自身判斷能力，在有證據時協助使用者擬稿通報。這是一種懷柔的資安設計：降低做好事的成本，而不是增加日常開發的負擔。

安裝後自動加入全域 CLAUDE.md 或 AGENTS.md，平常只保留簡短觸發提醒，遇到可疑網頁、指令或防毒警告才讀取本機 SKILL.md。使用者決定是否通報，不自動上傳。重複安裝不重複註冊，原有指令保留並備份。
