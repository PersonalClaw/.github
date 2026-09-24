<!--
Organization-wide PR template. Repositories with their own template override this one —
PersonalClaw core and PersonalClawApps both do, and theirs is the authority there.
-->

> [!IMPORTANT]
> **Every commit must be signed off**, or the DCO check fails. Commit with `git commit -s`.
> Already pushed without it? `git rebase --signoff main && git push --force-with-lease`.
> The sign-off name and email must match the commit author. See
> [CONTRIBUTING § DCO](https://github.com/PersonalClaw/PersonalClaw/blob/main/CONTRIBUTING.md#developer-certificate-of-origin-dco).

## What changed

<!-- One paragraph: what behaviour or content changed, and why. -->

## How you verified it

<!--
What you ran, and what it said. "pytest ." passing is enough for a small repo; say so
explicitly rather than leaving it blank. If you changed an app manifest, say that you
installed the app and drove it from the dashboard — a manifest that parses is not a
manifest that works.
-->

## Anything a reviewer should know

<!--
A pre-existing failure you did not cause (say so, with the result on `main` too), a
decision you were unsure about, or a follow-up you deliberately left out of scope.
Write "nothing" if there is nothing.
-->
