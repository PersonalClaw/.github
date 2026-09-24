<div align="center">

<img src="./assets/mark.png" alt="PersonalClaw" width="96" />

# PersonalClaw

**A self-hosted personal AI agent — an agentic operating system for one person.**

Chat, autonomous goal loops, long-term memory, a knowledge base, skills, scheduled
automation, and channel integrations — all behind **one gateway process** and **one web
dashboard you own**. Local-first, provider-agnostic, zero telemetry, MIT.

[![Core CI](https://github.com/PersonalClaw/PersonalClaw/actions/workflows/ci.yml/badge.svg)](https://github.com/PersonalClaw/PersonalClaw/actions/workflows/ci.yml)
[![PyPI](https://img.shields.io/pypi/v/personalclaw?label=PyPI&color=informational)](https://pypi.org/project/personalclaw/)
[![License: MIT](https://img.shields.io/badge/License-MIT-informational.svg)](https://github.com/PersonalClaw/PersonalClaw/blob/main/LICENSE)
[![Python 3.12+](https://img.shields.io/badge/python-3.12%2B-blue.svg)](https://github.com/PersonalClaw/PersonalClaw)
[![Zero telemetry](https://img.shields.io/badge/telemetry-none-brightgreen.svg)](https://personalclaw.dev)
[![Self-hosted](https://img.shields.io/badge/self--hosted-local--first-ff6b5b.svg)](https://personalclaw.dev)

[**Website**](https://personalclaw.dev) · [**Core**](https://github.com/PersonalClaw/PersonalClaw) · [**Apps**](https://github.com/PersonalClaw/PersonalClawApps) · [**Docs**](https://github.com/PersonalClaw/PersonalClaw/blob/main/docs/guides/getting-started.md) · [**Latest release**](https://github.com/PersonalClaw/PersonalClaw/releases/latest) · [**Discussions**](https://github.com/PersonalClaw/PersonalClaw/discussions)

<br />

<img src="./assets/screens/dashboard-dark.png" alt="The PersonalClaw dashboard — tasks, active work, and context-aware suggestions at a glance" width="85%" />

<sub><em>The dashboard — one home for tasks, active work, and context-aware suggestions. Dark theme shown; PersonalClaw ships light and dark.</em></sub>

</div>

---

## What is PersonalClaw?

PersonalClaw runs AI agents that accomplish **your** work with a rich, user-assembled set
of capabilities. Every vendor — model providers, search, speech, channels, agent
runtimes — is a **removable app**, so nothing ties you to a single LLM vendor or service.
All state lives under one `~/.personalclaw` home on your machine; the system degrades
gracefully to local-only and never requires the network for core operation.

It is deliberately **single-user and self-hosted**: your conversations, memory, and
knowledge never leave your machine unless *you* wire up a remote provider app. There is
**no telemetry** — not as a setting, but as an architectural choice.

```mermaid
flowchart TB
    U["👤 You — dashboard · CLI · channels"] --> GW["🦞 Gateway (one process)"]
    subgraph core["Provider-agnostic core"]
        GW --> CHAT["Agentic Chat"]
        GW --> LOOP["Goal Loops"]
        GW --> AUTO["Automation · Triggers · Inbox"]
        CHAT & LOOP & AUTO --> ENG["Context Engine · Approvals · Guardrails"]
        ENG --> MEM["Memory"]
        ENG --> KN["Knowledge"]
        ENG --> SK["Skills"]
    end
    ENG --> APPS["App Platform (permission-gated, scanner-gated)"]
    APPS --> P1["Model providers"]
    APPS --> P2["Search · Speech · Local models"]
    APPS --> P3["Channels · Agent runtimes (ACP)"]
    APPS -. "removable, sandboxed" .-> EXT[("Your vendors & tools")]
```

---

## The repositories — what to read first

**Start with [PersonalClaw](https://github.com/PersonalClaw/PersonalClaw).** It is the only
source of product truth: the apps repo follows it, and the website *projects* released core
state — it never advertises ahead of a real release. Everything else in this org exists
because core points at it.

### The product

| Repository | What it is |
|---|---|
| 🦞 **[PersonalClaw](https://github.com/PersonalClaw/PersonalClaw)** | The **platform** — the gateway, agentic core, memory, knowledge, skills, automation, security, and the permission-gated app platform. Python 3.12 · aiohttp · React + Vite SPA · SQLite. This is where every capability and contract originates. |
| 🧩 **[PersonalClawApps](https://github.com/PersonalClaw/PersonalClawApps)** | The **first-party app bundles** — 69 apps across model providers, search, speech, local models, agents (ACP), channels, tools, and full backend + UI apps. Each imports core **only** through the stable SDK and installs through the same scanner-gated Store as any third-party app. |
| 🌐 **[personalclaw.dev](https://github.com/PersonalClaw/personalclaw.dev)** | The **public website** — product, documentation, security, installation, and ecosystem surface. A zero-tracking, Astro-built projection of *released* PersonalClaw, pinned to exact core + apps revisions so it can never claim something the product can't back. |

### The community ecosystem

| Repository | What it is |
|---|---|
| 📋 **[registry](https://github.com/PersonalClaw/registry)** | The **community app list**. Core ships this repo's URL as a *removable* default git source, so listed apps appear in your Store next to any source you add yourself. It is a list, not a store and not an endorsement: every listing publishes its scanner verdict rather than being quietly curated by one. [Listing policy](https://github.com/PersonalClaw/registry/blob/main/CONTRIBUTING.md) · [delisting policy](https://github.com/PersonalClaw/registry/blob/main/DELISTING.md). |
| 📡 **[personalclaw-push-relay](https://github.com/PersonalClaw/personalclaw-push-relay)** | A **stateless, content-free** push relay for the mobile companion — it forwards ids-only wake-up pings to APNs/FCM and stores nothing. Self-hosted push (ntfy/UnifiedPush) needs no relay at all; this exists only because native APNs/FCM can be sent solely by whoever holds the app's signing credentials. Deploy your own. |

### Fork one of these to build an app

Four **exemplar apps**, one per provider contract, each installable through the Store from
its own git URL and each listed in the registry. They are deliberately tiny and
heavily commented — the README of each is a lesson in the contract it implements.

| Repository | Contract it teaches |
|---|---|
| 🕳️ **[channel-null](https://github.com/PersonalClaw/channel-null)** | `ChannelTransportProvider` — accepts every message, delivers none. The smallest honest transport, and the conformance baseline. |
| 📥 **[inbox-github-notifications](https://github.com/PersonalClaw/inbox-github-notifications)** | `MessageSourceProvider` — your GitHub notifications as inbox items. Stdlib only; teaches checkpoints and degrade-to-empty. |
| 👀 **[watched-source-github](https://github.com/PersonalClaw/watched-source-github)** | `TriggerSourceProvider` — watches repos, emits `new_release` / `new_issue`. Teaches the push contract and the first-observation high-water mark. |
| 🏠 **[action-home-assistant](https://github.com/PersonalClaw/action-home-assistant)** | `ActionProvider` — fires a Home Assistant webhook. Teaches validate-don't-raise and honest dry-run/reversal claims. |

The full contract is in the
[app creation guide](https://github.com/PersonalClaw/PersonalClawApps/blob/main/docs/app-creation-guide.md),
and `personalclaw app new --type <kind>` scaffolds a working app in one command.

---

## Highlights

<table>
<tr>
<td width="50%" valign="top">

### 🗣️ Agentic chat
Multi-session chat with tool use and approval controls, session forking/undo, answer
variants, folders/tags/kanban, side conversations, per-session model overrides, and
temporary/incognito memory modes.

</td>
<td width="50%" valign="top">

### 🎯 Goal loops
Give the agent a target and let it work autonomously — it classifies the goal, plans it,
then loops cycle by cycle under a **deterministic supervisor** you can pause, nudge, or
stop.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🧠 Memory that learns
Layered semantic + episodic + procedural memory with active recall, after-turn learning
from your corrections, automatic promotion of repeated facts, and an optional
Obsidian-compatible markdown vault.

</td>
<td width="50%" valign="top">

### 📚 Knowledge base
Ingest documents (PDF/DOCX/PPTX/HTML/…), web pages, and media; AI enrichment, entity
extraction, a knowledge graph, and semantic search wired straight into chat context.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🧩 Skills & app platform
Reusable `SKILL.md` procedures plus a permission-gated **Store** where providers,
channels, agent runtimes, and full backend + UI apps install through a
quarantine → scan → consent lifecycle.

</td>
<td width="50%" valign="top">

### ⏰ Automation
Cron / interval / webhook triggers, background subagents, an inbox that watches channels
and drafts replies, and workflow SOPs surfaced automatically when they match.

</td>
</tr>
</table>

### 🛡️ Security-first, by construction
Tool approval modes, a shell-command denylist, an egress guard with allow/deny host
policy, a tamper-evident (HMAC) security event log, app-scoped tokens, and honest labeling
of the one permission it can't technically enforce. Controls are enforced **at the point
of execution**, not merely requested in a prompt — the
[threat model](https://github.com/PersonalClaw/PersonalClaw/blob/main/docs/security/threat-model.md)
maps each to the OWASP Agentic Top-10 with code citations and states the limitations
plainly.

<div align="center">
<table>
<tr>
<td><img src="./assets/screens/chat-light.png" alt="Agentic chat, grounded in your knowledge — light theme" /></td>
<td><img src="./assets/screens/loops-dark.png" alt="An autonomous goal loop mid-run under a deterministic supervisor" /></td>
</tr>
<tr>
<td><img src="./assets/screens/knowledge-dark.png" alt="Knowledge base with source documents and an entity graph" /></td>
<td><img src="./assets/screens/memory-light.png" alt="Layered, inspectable memory that learns how you work" /></td>
</tr>
</table>
<sub><em>Chat · goal loops · knowledge · memory — the full showcase (every screen, light and dark) lives in the <a href="https://github.com/PersonalClaw/PersonalClaw/blob/main/SHOWCASE.md">core repo</a>.</em></sub>
</div>

---

## Quickstart

Install with one command — every path installs the **same release artifact**, and you
don't need to install Python or Node yourself:

```bash
uv tool install personalclaw && personalclaw setup     # recommended — uv brings Python 3.12
```

Or use the bootstrap one-liner (installs `uv` if it's missing, then the above):

```bash
curl -fsSL https://personalclaw.dev/install | sh
```

Then start the gateway and open the dashboard at `http://localhost:10000`:

```bash
personalclaw gateway
```

Install a model-provider app from the Store, add your API key under **Settings →
Providers**, and bind a chat model under **Settings → Models**. Full walkthrough in
[Getting started](https://github.com/PersonalClaw/PersonalClaw/blob/main/docs/guides/getting-started.md).
Also available via **pipx**, **pip** (into an existing Python 3.12+ venv), **Docker
Compose**, or a **git checkout** for development.

Which version you just installed, what changed in it, and its SBOM and provenance
attestations are all on the
[latest release](https://github.com/PersonalClaw/PersonalClaw/releases/latest); the
running history is in the
[changelog](https://github.com/PersonalClaw/PersonalClaw/blob/main/CHANGELOG.md).

<div align="center">
<img src="./assets/screens/apps-dark.png" alt="The permission-gated app Store — providers, search, channels, agents, and full apps" width="80%" />
<br />
<sub><em>The Store — 69 first-party apps, each installed through a quarantine → security-scan → consent lifecycle.</em></sub>
</div>

---

## ⚠️ Pre-1.0 — breaking changes expected

PersonalClaw follows a **clean-break** engineering doctrine: when a design is replaced,
the old path is removed in the same change rather than carried behind compatibility shims.
The upshot for early users:

- The next few minor (0.x) releases may introduce **breaking changes with no automatic
  migration** of your existing data under `~/.personalclaw`.
- **Back up before every update** — `personalclaw snapshot` creates a portable archive
  (restore with `personalclaw restore`).
- Treat anything you put in PersonalClaw as reproducible or backed up elsewhere until
  backward-compatibility becomes the default posture. The migration-backed regime —
  gated changes that carry your data forward — is deliberately deferred until the
  architecture stops moving, on the way to 1.0; the reasoning is in
  [CONTRIBUTING § the lifecycle mental model](https://github.com/PersonalClaw/PersonalClaw/blob/main/CONTRIBUTING.md#the-lifecycle-mental-model).

We'd rather tell you plainly now than surprise you on an update.

---

## Contributing — where does my thing go?

| You want to… | Go here |
|---|---|
| **Ask a question**, show what you built, or float an idea | [Discussions](https://github.com/PersonalClaw/PersonalClaw/discussions) — one home for the whole org |
| **Report a bug** in the gateway, dashboard, CLI, memory, knowledge, or security | [core issues](https://github.com/PersonalClaw/PersonalClaw/issues/new/choose) |
| **Report a bug in a first-party app** (a provider, channel, or agent bundle) | [apps issues](https://github.com/PersonalClaw/PersonalClawApps/issues/new/choose) |
| **Get your app listed** so others can install it | one PR adding a row to [registry](https://github.com/PersonalClaw/registry) — read its [listing policy](https://github.com/PersonalClaw/registry/blob/main/CONTRIBUTING.md) first; every rule is enforced by CI, not by review |
| **Write an app** | fork the exemplar for your contract (above), then the [app creation guide](https://github.com/PersonalClaw/PersonalClawApps/blob/main/docs/app-creation-guide.md) and [platform architecture](https://github.com/PersonalClaw/PersonalClawApps/blob/main/docs/platform-architecture.md) |
| **Change core** | the [contributing guide](https://github.com/PersonalClaw/PersonalClaw/blob/main/CONTRIBUTING.md) — engineering doctrine (clean break, provider-agnostic core, validate-as-a-user), dev setup, and the definition of done |
| **Report a security issue** | **privately**, never as a public issue — [security policy](https://github.com/PersonalClaw/PersonalClaw/blob/main/SECURITY.md) |

Every commit needs a `Signed-off-by` line (`git commit -s`) — CI enforces the
[DCO](https://github.com/PersonalClaw/PersonalClaw/blob/main/CONTRIBUTING.md#developer-certificate-of-origin-dco).
Running `npm install` once in your clone installs the hooks that add it for you.

**Supply chain.** Releases build in CI from a committed lockfile; PyPI publishing uses
Trusted Publishing (OIDC) behind a manual approval gate; every release ships a syft SBOM
and build-provenance attestations.

---

<div align="center">

**[Get started at personalclaw.dev »](https://personalclaw.dev)**

Open source · self-hosted · zero telemetry · [MIT](https://github.com/PersonalClaw/PersonalClaw/blob/main/LICENSE)

</div>
