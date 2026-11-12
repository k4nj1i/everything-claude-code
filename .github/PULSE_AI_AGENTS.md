# Pulse: GitHub coding agents (12 November 2026)

This repository supports three summonable coding agents after the relevant
workflows are merged to the default branch. Do not mistake a workflow file
for an authenticated, activated service.

| Agent | How to call | Status and credentials |
| --- | --- | --- |
| Claude Code | `@claude` on an issue or PR comment | Existing Claude workflow or added `.github/workflows/claude.yml`; needs `CLAUDE_CODE_OAUTH_TOKEN` or `ANTHROPIC_API_KEY`. |
| OpenAI Codex | `@codex` on an issue or Actions > Pulse Codex | Gated off by default; needs `OPENAI_API_KEY` and repository variable `PULSE_CODEX_ENABLED=true`. |
| Qwen Code | `@qwencoder` on an issue or Actions > Pulse Qwen | Gated off by default; needs `QWEN_API_KEY` and repository variable `PULSE_QWEN_ENABLED=true`. |

Codex and Qwen respond to issue text/comments and owner-launched manual workflow
runs. They do **not** respond to PR comments in this initial configuration.
They may propose changes as a **new pull request**, but must never self-merge.
An optional `PULSE_PR_TOKEN` secret can be used if PRs authored by the
standard GitHub Actions token do not trigger required CI; do not create one
with broader privileges than necessary. Ensure the repository permits GitHub
Actions to create pull requests before enabling the agents.

## Activation checklist (each repository separately)

1. Confirm the provider, privacy terms, and genuine free usage allowance or
   obtain explicit studio spend approval. An OpenAI ChatGPT subscription does
   not automatically provide API credits. Do not activate metered usage by assumption.
2. Add the provider key in **Settings > Secrets and variables > Actions**.
   Never commit keys, tokens or login data to source control.
3. For Codex or Qwen only, add the matching enabled repository **variable**
   (`PULSE_CODEX_ENABLED` or `PULSE_QWEN_ENABLED`) set to `true` after approval.
4. On a non-sensitive issue, invoke exactly one agent and check the result,
   branch, pull request, green checks, independent review, and actual cost.
5. Keep all existing Team rules, AGENTS.md, deployment approvals, security
   protections and project-specific restrictions. Never use real athlete data,
   personal information or production secrets in external-agent prompts.

## Additional model options

GitHub Copilot's cloud agent can be assigned to an issue where a paid Copilot
plan and repository permissions enable it; some models (e.g. Kimi/Grok) can
be selected through Copilot subject to entitlement. DeepSeek, Mistral, Kimi
and Gemini do not gain a working standalone @mention merely by adding them
to a document. Any future integration needs its own supported workflow,
credentials, and a verified spend/privacy route.

## Sources

- https://github.com/anthropics/claude-code-action
- https://github.com/openai/codex-action
- https://github.com/QwenLM/qwen-code-action
- https://docs.github.com/en/copilot/how-tos/copilot-on-github/use-copilot-agents/overview
