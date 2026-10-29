---
name: complete-browser-task
description: Complete an authorized website workflow by coordinating navigation, clicking, form filling, asynchronous waits, recovery and outcome verification. Use for multi-step web forms, dashboard configuration, submissions, bookings, account setup, or resuming a stalled browser task. Use when the user asks to finish a browser task autonomously or bundle its steps into one workflow. Prefer sufficient service connectors; use TinyFish or an available browser when interaction is needed. This skill does not supply a browser, credentials or extra permissions.
---

# Complete browser task

Own the requested outcome across tool calls. Carry existing authorization forward; do not ask the user to approve routine navigation, field entry, waits or already-authorized submission again. Respect all higher-priority permissions, tool restrictions and explicit user boundaries.

## 1. Define the result

Extract a compact task contract from the conversation; do not turn it into a questionnaire:

- Target site, exact resource and requested account scope.
- Requested result and separately authorized side effects, including whether submission is authorized.
- Required inputs, privacy restrictions and existing work to preserve.
- Observable success evidence for each milestone.

Resolve nonessential choices using sensible defaults. Never invent required factual answers. Complete useful independent work before asking for an essential missing input. Do not send messages to other people without explicit authorization. Prepare a reviewable result before any independently required approval.

Distinguish stages such as prepared, submitted, accepted, verified, processed and effective. A click or a completed automation run does not prove the requested outcome.

## 2. Select an execution route

Inspect available capabilities and their current documentation before use.

1. Follow the user's explicit tool/environment choice when supported.
2. Otherwise prefer a sufficient service-specific connector or supported API.
3. For browser interactions, inspect applicable saved profiles/session metadata before initiating login. Match the site and authorized account scope; a friendly profile name alone does not prove sign-in.
4. Reuse an applicable signed-in session within the provider's documented mechanism. Do not extract cookies, credentials or tokens or transfer them across tools. A saved sign-in may have expired.
5. Use TinyFish for a supported, bounded website workflow when available and appropriate; read [references/tinyfish.md](references/tinyfish.md). Otherwise use the selected browser's skill and documented API.

Do not equate one browser's authentication timeout with a global inability to do the task. Check other already-authorized, suitable routes when their rules permit it. If a provider requires approval before fallback, obtain it; do not use tool switching to bypass an access denial, CAPTCHA, quota or security control. Distinguish a different valid session from circumventing a restriction.

## 3. Execute toward checkpoints

Give a brief progress update, then execute dependent steps sequentially. Batch independent read-only checks when supported. Keep distinct websites or tasks separate unless the provider explicitly supports the workflow.

For an autonomous browser tool, send a concrete goal containing the target, necessary inputs, authorized actions, success criteria and stop conditions. Do not send a long speculative sequence of coordinates or selectors. For a direct browser, use an observe → act → observe loop grounded in the current page. Re-read after navigation, modal changes or failures; do not reuse stale selectors blindly.

Fill and validate fields, resolve routine validation errors, submit only within authorization, then inspect the confirmation or resulting resource. Before retrying a side-effecting step after timeout, determine whether it already succeeded. Check the destination record/history or a provider-supported idempotency key; never duplicate a submission just because confirmation was missed.

Keep a minimal task checkpoint in the active workspace for long or interrupted work:

```text
Target and authorized scope:
Execution provider and opaque run/resource ID:
Completed milestones and observed evidence:
Last observed state:
Submission state: not attempted | confirmed | uncertain
Next safe step:
Blocker, if any:
```

Keep checkpoints private. Exclude passwords, OTPs, cookies, access tokens, personal identifiers, signed URLs and sensitive form contents. Record only necessary operational IDs; do not publish them. Reuse the checkpoint after interruptions rather than restarting.

## 4. Wait and recover deliberately

Use provider wait/status operations for asynchronous work. Keep the original run ID. A timeout may mean work is still executing. Follow the provider's exact polling/recovery contract; do not launch a duplicate run. Use bounded waits and concise progress updates during long tasks, ordinarily within 60 seconds. Stop polling when the run is terminal; inspect its actual result.

Classify the obstacle before choosing the next action:

| Observation | Next action |
| --- | --- |
| Stale UI, modal or field validation error | Refresh observed state; correct the specific issue within scope. |
| Running job or transport timeout | Resume/check the same job through supported tools. |
| Uncertain submission | Inspect existing records before considering any retry. |
| External prerequisite, e.g. a verification tag must be deployed | Capture exact provider-issued artifact, perform authorized prerequisite, independently check it, then start the next stage. |
| One tool lacks a capability or session | Check a permitted alternative using its own valid access; preserve task state. |
| Login, MFA or CAPTCHA | Use documented secure authentication or user handoff. Never request secrets in chat or work around the challenge. |
| Explicit permission denial or account mismatch | Stop the denied action, retain completed work, explain exact missing authorization. |
| Provider credits or quota exhausted | Follow the provider's required next step. Do not retry repeatedly, buy credits without authorization, or switch identities to evade limits. |
| Missing essential factual input | Finish independent work, then ask one focused question. |

Retry only when an observed change or a specific corrective action supports it. After one targeted correction, reassess; avoid repeating the same failing call. A terminal run that completed an intermediate stage may be followed by a new, nonduplicative stage. A failed or still-running submission must not be blindly restarted.

## 5. Verify and finish

Check the destination's actual state, not only the automation agent's summary. Prefer a confirmation screen, resulting record ID/status, read-back through an authorized connector, or independent public response where relevant. If only a provider's reported observation is available, identify that evidence source and retain its limits; do not claim an independent visual check.

Compare every required milestone to the task contract. Resolve concrete failures within scope; stop optional checks once sufficient. Record partial success and unknowns separately. For deployment/Search Console work, also follow the publish-cloudflare-search-console skill: public reachability, ownership verification, sitemap submission, sitemap processing and indexing are distinct outcomes.

Finish with the result, a useful link, what was verified, and any exact remaining blocker. If user action is essential, explain why and give the smallest documented next step. Do not promise a later retry or monitoring unless an automation was actually created with authorization.
