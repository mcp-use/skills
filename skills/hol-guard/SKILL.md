---
name: hol-guard
description: Protect supported local AI coding harnesses with HOL Guard before tool execution. Use for local agent runtime safety, protected coding-agent launch, Guard approvals, receipts, and fail-closed verification.
license: Apache-2.0
compatibility: Requires Python 3.10+, pipx, and a HOL Guard-supported local coding harness. Network access to PyPI is needed for first install.
metadata:
  author: HOL
  version: "1.0.0"
  category: security
allowed-tools: Bash(*) Read Grep Glob
---

# HOL Guard

Use HOL Guard as an additional local runtime-safety layer before a supported coding agent performs mutation-bearing work. Keep the agent's native authentication, permissions, confirmations, sandboxing, and provider controls enabled.

## Safety contract

- Never claim protection unless HOL Guard itself reports a healthy result for the detected harness.
- Never guess a harness identifier. Use `hol-guard detect --json` and the exact supported identifier it returns.
- If detection, bootstrap, install, dry-run, doctor, or status fails, stop mutation-bearing work. Do not fall back to the raw harness binary.
- Do not approve blocked work implicitly. Inspect the Guard risk reason and preserve the request ID.
- Keep Guard Cloud optional. Do not connect or sync unless the user explicitly asks for it.
- Do not weaken native agent controls because Guard is installed.

## Install stable HOL Guard

Probe the CLI first:

```sh
hol-guard --version
```

If the command is unavailable and the user asked to install Guard, install the validated stable release reproducibly:

```sh
pipx install --force "hol-guard==3.0.18"
hol-guard --version
```

Do not substitute a prerelease unless the user explicitly asks to test one.

## Detect and protect the local harness

Run from the target workspace:

```sh
hol-guard status
hol-guard detect --json
```

Select only an exact supported harness identifier returned by detection. Then use the Guard-owned protection flow:

```sh
hol-guard bootstrap
hol-guard install <harness>
hol-guard run <harness> --dry-run
hol-guard doctor <harness> --json
hol-guard run <harness>
hol-guard status
```

The dry run and `doctor` must succeed before protection is claimed. Keep the final status output as current posture evidence.

If detection finds no supported harness, or any protection step fails, stop. Report the exact failure instead of launching an unprotected agent session.

## Handle blocked or approval-gated work

Inspect Guard-owned decisions and evidence:

```sh
hol-guard approvals
hol-guard approvals open <request-id>
hol-guard receipts
hol-guard diff <harness>
```

Use the exact pending request ID returned by `hol-guard approvals` when opening its approval page.

When Guard returns a request ID and the user makes a terminal decision:

```sh
hol-guard approvals approve <request-id>
hol-guard approvals deny <request-id>
```

A prior approval does not authorize a different request. Never invent an approval or request ID.

## Audit evidence

Use Guard's own evidence surfaces:

```sh
hol-guard receipts
hol-guard inventory
hol-guard abom --format json
hol-guard events
hol-guard status
```

Report only evidence that Guard actually returned.

## Data boundary

The local protection flow does not require a Guard Cloud account. Installing the Python package downloads the named distribution from PyPI. Do not send source files, prompts, completions, environment files, credentials, or secret stores to a third party merely to complete this skill.

If the user explicitly requests Guard Cloud connection or sync, inspect current connection state and explain the synchronization boundary before enabling it.

## Remove HOL Guard

Use Guard's documented removal path instead of manually deleting managed harness configuration:

```sh
hol-guard uninstall --self
```

Verify the resulting state before claiming cleanup succeeded.

## Output

Return a concise protection report with the detected harness identifier, HOL Guard version, bootstrap/install/dry-run/doctor/run results, final status evidence, any pending approvals, whether optional cloud sync remained disabled, and the exact next safe command when work remains blocked.
