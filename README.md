# Mermail Inbox Safety Review for Codex

A reusable, read-only Codex skill that reviews user-selected Mermail emails for instructions aimed at an AI agent. It reports evidence, exact Mermail message IDs, scan status, and sender authentication status. It does not change the inbox or declare an email definitively safe or fraudulent.

[Watch the 2–5 minute demo on X](https://x.com/Detoxin01/status/2105715368513978867?s=20) · [Upstream Mermail skills contribution](https://github.com/Nudgen-Marketing/mermail-skills/pull/432)

## What is in this repository

- `SKILL.md` — the review workflow and boundaries.
- `references/tools.md` — bounded Mermail MCP reads and tool parameters.
- `references/security.md` — how to handle email content as untrusted data.
- `agents/openai.yaml` — Codex display information and Mermail MCP dependency.

## Install in Codex

Codex looks for a personal skill at `~/.agents/skills/<skill-name>/SKILL.md`. Clone this repository directly into that location. On Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.agents\skills" | Out-Null
git clone https://github.com/Detoxin01/mermail-inbox-safety-review.git "$HOME\.agents\skills\mermail-inbox-safety-review"
```

On macOS or Linux:

```sh
mkdir -p ~/.agents/skills
git clone https://github.com/Detoxin01/mermail-inbox-safety-review.git ~/.agents/skills/mermail-inbox-safety-review
```

Codex usually detects a newly installed skill automatically. Restart it if the skill does not appear. You can explicitly invoke it with `$mermail-inbox-safety-review`.

## Connect Mermail

The skill provides instructions; Mermail MCP provides the mailbox tools. Set up the focused agent-inbox connection and complete OAuth in Codex CLI:

```powershell
codex mcp add mermail --url "https://console.mermail.app/mcp?profile=agent-inbox"
codex mcp login mermail
codex mcp list
```

If `mermail` is already connected, use that connection. Do not put an API key in a prompt or in this repository. The skill stops if it cannot access scan-safe Mermail reads.

## Try it

```text
Use $mermail-inbox-safety-review to review the “Workshop schedule” and “Test instruction” emails in etix01@mermail.app. Report exact message IDs, scan and sender-authentication status, evidence, and your assessment. Do not change the inbox.
```

In the recorded test, the workshop message had no observed agent-directed instruction. The test message told the agent to ignore the user's request and was marked for review. Both scan results were clean, sender authentication was unknown, and no mailbox changes were made. These are observations from that test, not promises about future messages.

## License

MIT. See [LICENSE](LICENSE). This standalone copy is based on the Mermail skills repository and retains its copyright notice.
