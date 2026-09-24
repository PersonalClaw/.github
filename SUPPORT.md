# Getting help

PersonalClaw is maintained by one person. That shapes the honest answer to "where do I ask?"
— use the surface that lets the answer help the next person too.

## Start here

| Your situation | Best surface |
|---|---|
| "How do I…?", "Is this supposed to…?", "Which app should I use for…?" | [Discussions → Q&A](https://github.com/PersonalClaw/PersonalClaw/discussions/categories/q-a) |
| "Here's what I built / my setup" | [Discussions → Show and tell](https://github.com/PersonalClaw/PersonalClaw/discussions/categories/show-and-tell) |
| "It should do X instead" | [Discussions → Ideas](https://github.com/PersonalClaw/PersonalClaw/discussions/categories/ideas) |
| "I'm writing an app and the contract is unclear" | [Discussions → App Dev](https://github.com/PersonalClaw/PersonalClaw/discussions/categories/app-dev) |
| "This is broken and I can reproduce it" | an [issue](https://github.com/PersonalClaw/PersonalClaw/issues/new/choose) in the repo that owns it |
| "I found a security flaw" | **privately** — [SECURITY.md](SECURITY.md). Never a public issue. |

## Before you ask

Most questions are answered faster by one of these than by waiting for a reply:

- **[Getting started](https://github.com/PersonalClaw/PersonalClaw/blob/main/docs/guides/getting-started.md)** —
  install, first run, binding a model, installing your first app.
- **`personalclaw doctor`** — checks your install and names what is wrong, including
  provider bindings, ports, and home-directory state. Run it before filing anything.
- **The [latest release notes](https://github.com/PersonalClaw/PersonalClaw/releases/latest)** —
  PersonalClaw is pre-1.0 and 0.x releases may break data without migration, so "it stopped
  working after an update" is often answered there.
- **[Docs](https://github.com/PersonalClaw/PersonalClaw/tree/main/docs)** and
  **[personalclaw.dev](https://personalclaw.dev)**.

## What makes a report answerable

Whichever surface you use, include the version (`personalclaw --version`), how you
installed, your OS, and what you actually did versus what happened. **Redact before you
paste** — agent logs and config can carry API keys, tokens, and private file paths.
