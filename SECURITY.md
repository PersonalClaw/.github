# Security Policy — the PersonalClaw organization

This policy covers **every repository in this organization** that does not publish its
own. The core platform's policy, which is more detailed because the platform has far more
attack surface, is the authority for core:
[PersonalClaw/SECURITY.md](https://github.com/PersonalClaw/PersonalClaw/blob/main/SECURITY.md).

## Reporting a vulnerability

**Report privately — do not open a public issue.**

Use GitHub's private vulnerability reporting on the
[core repository's Security tab](https://github.com/PersonalClaw/PersonalClaw/security)
and click **"Report a vulnerability"**. That opens an advisory visible only to you and the
maintainer. Report there even when the flaw is in a smaller repo in this org — one intake
means nothing gets lost in a repo nobody watches.

Include, where you can:

- **which repository and component** the flaw is in;
- the impact, and a proof-of-concept or reproduction steps;
- the version, tag, or commit you observed it on.

## What to expect

PersonalClaw is maintained by a single person, so these are honest expectations, not
contractual SLAs:

- **Acknowledgement within 7 days.**
- **A fix or a remediation plan within 30 days** for confirmed issues.

If a report stalls past those windows, a polite nudge on the advisory thread is welcome.

## Scope notes for this org's smaller repositories

- **[registry](https://github.com/PersonalClaw/registry)** — the listings are data, and a
  listed app is *not* vetted code. A malicious listed app is handled by the
  [delisting policy](https://github.com/PersonalClaw/registry/blob/main/DELISTING.md),
  which is the faster path than an advisory. A flaw in the *validator* — something that
  lets a listing bypass the scanner dry-run — is a vulnerability: report it.
- **The exemplar apps** (`channel-null`, `inbox-github-notifications`,
  `watched-source-github`, `action-home-assistant`) — these are reference code people
  fork. A flaw that a forker would inherit is worth reporting even though the exemplar
  itself handles little.
- **[personalclaw-push-relay](https://github.com/PersonalClaw/personalclaw-push-relay)** —
  its whole security claim is that it is stateless and content-free. Any path that gets
  content or state through it is a vulnerability, including a log line that carries more
  than `platform`, `kind`, `item_id`, and the vendor status.

## What is not a vulnerability here

PersonalClaw deliberately runs an autonomous agent with real capabilities on your own
machine. Behaviour that is a *documented* consequence of a permission you granted is not a
vulnerability — the boundary, and the one permission the platform cannot technically
enforce, are stated plainly in the
[threat model](https://github.com/PersonalClaw/PersonalClaw/blob/main/docs/security/threat-model.md)
and [limitations](https://github.com/PersonalClaw/PersonalClaw/blob/main/docs/security/limitations.md).
Read those first; if the behaviour you found is *not* in them, that gap is itself worth
reporting.
