# Pulse — Coding agents for GitHub (12 November 2026)

Four agent workflow entrypoints are represented in this repository's setup
PR. A workflow checked into source control is NOT evidence that the provider
has been connected, authenticated, paid for, or successfully run.

## Two distinct forms of Codex access

**Subscription-backed Codex Cloud**: Use your ChatGPT subscription (subject
to plan access and usage quotas). Sign in at https://chatgpt.com/codex,
connect the GitHub account through Codex's GitHub authorization, choose the
repositories and create/publish cloud environments. This **does not** enable
an `@codex` GitHub issue-comment responder. That is a separate integration
requiring an OpenAI API credential in the official GitHub Action.

**Pulse on-demand Codex GitHub workflow**: `.github/workflows/pulse-codex.yml`
responds to `@codex` in an authorised issue comment or via manual Actions run.
It remains **disabled by default**. Activation requires an explicitly approved
`OPENAI_API_KEY` secret AND repository variable `PULSE_CODEX_ENABLED=true`.
No assumption that a ChatGPT Plus/Pro subscription pays for Actions API usage.
Never set this variable without confirmed permitted API costs.

## Gemini: monthly subscription is not unattended GitHub API access

As of 18 June 2026, consumer Google AI Pro/Ultra accounts migrated from
Gemini CLI to Antigravity CLI for subscription-backed terminal coding.
The old consumer Gemini Code Assist on GitHub also shut down. Use your
consumer subscription with the Google Antigravity tooling, not a GitHub
`GEMINI_API_KEY` secret. Don't paste a Google account password or browser
session token into GitHub Actions.

**Pulse on-demand Gemini GitHub workflow**: `.github/workflows/pulse-gemini.yml`
responds to `@gemini-cli` on an authorised GitHub issue or via manual Actions run.
It uses Google's official `run-gemini-cli` GitHub Action with an API key, NOT
the Google AI Pro/Ultra subscription. It remains **disabled by default**.
Activation requires:
- Confirm this repository has no confidential personal, athlete, unreleased,
  client, or security-sensitive data exposed to the chosen API's free tier.
- Choose a verified eligible Google AI Studio free-tier model with billing
  disabled and suitable data-use terms. Free-tier content may be used to
  improve Google's products; do not opt into this for sensitive repositories.
- Add a `GEMINI_API_KEY` GitHub Actions secret.
- Set repository variable `PULSE_GEMINI_ENABLED=true` only after approval,
  then run ONE low-risk test issue and inspect usage, output and CI.
- Do not mistake this setup for automatic PR review; it is an on-demand issue
  coding workflow. Do not enable scheduled tasks or automatic model runs.

## Existing Claude and Qwen workflows

| Agent | GitHub trigger | Credential / gate |
| --- | --- | --- |
| Claude Code | `@claude` | `CLAUDE_CODE_OAUTH_TOKEN` or `ANTHROPIC_API_KEY`; existing workflows preserved |
| Qwen Code | `@qwencoder` on an issue | `QWEN_API_KEY` + `PULSE_QWEN_ENABLED=true`; disabled until authorised |
| Codex Action | `@codex` on an issue | `OPENAI_API_KEY` + `PULSE_CODEX_ENABLED=true`; disabled until authorised |
| Gemini Action | `@gemini-cli` on an issue | `GEMINI_API_KEY` + `PULSE_GEMINI_ENABLED=true`; disabled until authorised |

For on-demand agent PR creation, the optional `PULSE_PR_TOKEN` permits
GitHub Actions to create a PR that can trigger subsequent CI where the default
`GITHUB_TOKEN` would not. Require the narrowest privileges. No agent has
permission to self-merge, deploy, edit production data, change policies,
or purchase services. Continue to follow AGENTS.md, current Team rules, and
project-specific security/privacy requirements.

## Where to finish setup

- Codex Cloud subscriber authorization: https://chatgpt.com/codex
- Google Antigravity subscription coding: https://antigravity.google/
- Google API free tier and data-use terms: https://ai.google.dev/gemini-api/docs/pricing
- GitHub Actions secrets and variables: `Settings > Secrets and variables > Actions`
- Official Codex Action: https://github.com/openai/codex-action
- Official Gemini Action: https://github.com/google-github-actions/run-gemini-cli

**Current state in this branch:** workflow files added; no external
subscriptions, OAuth approvals, secrets, billing or live model tests
were provisioned by committing these files. Merge and verify in each repo.
