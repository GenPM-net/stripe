# @core/stripe

[![genpm](https://api.genpm.net/v1/badge/@core/stripe.svg)](https://genpm.net/p/@core/stripe) ![license](https://img.shields.io/badge/license-MIT-blue)

> Shared Stripe client and one idempotent, signature-verified webhook endpoint dispatching events to every module

A [GenPM](https://genpm.net) module: **source code + AI rules + MCP config**, injected into your project instead of hidden in `node_modules`. The code lands in `src/lib/stripe`, pinned to a verified commit, and you own it.

## Install

```bash
genpm add @core/stripe
```

No genpm yet? `curl -fsSL https://genpm.net/install.sh | sh` (macOS/Linux), `irm https://genpm.net/install.ps1 | iex` (Windows), or one-off with `npx @genpm-net/cli add @core/stripe`.

Or let your AI agent do it: run `genpm mcp setup` once, then ask *"add @core/stripe with genpm"* in Claude Code, Cursor, VS Code, Windsurf, Codex or Gemini CLI. It shows you a dry-run plan before writing anything.

## What it does

The single Stripe integration point of the app: a lazily created client (`getStripe`) and ONE webhook endpoint that
verifies the signature, records each event in `stripe_events` (idempotency) and dispatches it, inside one database
transaction, to the handlers that modules register with `onStripeEvent` (@core/billing 2.x, @core/checkout…).
If a handler throws, everything rolls back and Stripe retries. No business logic here.

## At a glance

- **GenPM dependencies** (installed with it): [@core/db](https://genpm.net/p/@core/db)
- **npm dependencies** (proposed, never installed without asking): `stripe`
- **Environment variables** (added to `.env.example`): `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`
- **MCP servers** (only added with your consent): `stripe`
- **AI rules**: [`AGENTS.md`](AGENTS.md), loaded by your agent only when it works in `src/lib/stripe`

## Security

GenPM installs a 40-character commit SHA (never a branch), verifies an Ed25519-signed manifest, never runs install scripts and scans AI rules for prompt injection. Details: [genpm.net/docs/security](https://genpm.net/docs/security).

## License

MIT — see [LICENSE](LICENSE). Browse the full catalog at [genpm.net](https://genpm.net).
