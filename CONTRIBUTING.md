# Contributing to PersonalClaw

This is the organization-wide guide. It exists to **route you to the right repository**,
because PersonalClaw is one product spread across several, and filing in the wrong place is
the most common way a good contribution stalls.

Repositories that publish their own `CONTRIBUTING.md` override this file. Two do, and both
are the authority for their own tree:

- **[PersonalClaw](https://github.com/PersonalClaw/PersonalClaw/blob/main/CONTRIBUTING.md)** —
  the platform. Engineering doctrine, dev setup, testing expectations, definition of done.
- **[registry](https://github.com/PersonalClaw/registry/blob/main/CONTRIBUTING.md)** — the
  listing policy for the community app list. Every rule in it is enforced by CI rather than
  by review, so read it before opening a listing PR.

## Where does my thing go?

| You want to… | Go here |
|---|---|
| Ask a question, show what you built, float an idea | [Discussions](https://github.com/PersonalClaw/PersonalClaw/discussions) — one home for the whole org |
| Report a bug in the gateway, dashboard, CLI, memory, knowledge, skills, or security | [core issues](https://github.com/PersonalClaw/PersonalClaw/issues/new/choose) |
| Report a bug in a first-party app bundle (a provider, channel, or agent) | [apps issues](https://github.com/PersonalClaw/PersonalClawApps/issues/new/choose) |
| Report a bug on the website | [personalclaw.dev issues](https://github.com/PersonalClaw/personalclaw.dev/issues) |
| Get your app listed so others can install it | a PR adding one row to [registry](https://github.com/PersonalClaw/registry) |
| Write an app | fork the exemplar for your provider contract, then read the [app creation guide](https://github.com/PersonalClaw/PersonalClawApps/blob/main/docs/app-creation-guide.md) |
| Report a security issue | **privately** — see [SECURITY.md](SECURITY.md). Never a public issue. |

**Building an app?** Fork the exemplar that matches your contract rather than starting
blank — each is a few hundred lines and its README is a lesson in the contract:
[channel-null](https://github.com/PersonalClaw/channel-null) (`ChannelTransportProvider`),
[inbox-github-notifications](https://github.com/PersonalClaw/inbox-github-notifications)
(`MessageSourceProvider`),
[watched-source-github](https://github.com/PersonalClaw/watched-source-github)
(`TriggerSourceProvider`),
[action-home-assistant](https://github.com/PersonalClaw/action-home-assistant)
(`ActionProvider`).

## Rules that hold in every repository here

1. **Sign off every commit.** `git commit -s` adds the `Signed-off-by` line the
   [DCO](https://github.com/PersonalClaw/PersonalClaw/blob/main/CONTRIBUTING.md#developer-certificate-of-origin-dco)
   check requires. CI fails without it. In core and the apps repo, `npm install` once
   installs a hook that adds it for you. Forgot on commits you already pushed?
   `git rebase --signoff main && git push --force-with-lease`.
2. **One concern per branch and per PR.** A PR that fixes a bug and also reformats a file
   is two PRs.
3. **Branch, never commit to `main`.** `main` is append-only and is never force-pushed.
4. **Run the repo's own gate before you push.** Each repo states it: `make lint` plus tests
   in core, `npm run test:ci` on the website, `pytest .` in an app repo. Remote CI is
   confirmation, not discovery.
5. **Don't weaken a check to make it pass.** A red assertion, budget, accessibility rule,
   or visual tolerance gets root-caused, not relaxed. If a failure is pre-existing on
   `main`, say so in the PR with both results.
6. **Say what you validated as a user**, not only what you wrote. "The endpoint returns
   200" is not validation; driving the flow in the UI or CLI is.
7. **Never commit secrets** — no API keys, tokens, device tokens, or the contents of a real
   `~/.personalclaw` home. If you already pushed one, treat it as leaked: rotate it first,
   then rewrite history.

## Code of Conduct

Participation in every space in this organization is governed by the
[Code of Conduct](CODE_OF_CONDUCT.md).
