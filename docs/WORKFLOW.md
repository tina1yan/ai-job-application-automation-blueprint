# Workflow and recovery contract

This document expands the reference workflow without prescribing a specific browser or model vendor.

## Source precedence

When records conflict, use an explicit order such as:

1. the applicant's current instruction;
2. active, verified facts in the canonical private fact bank;
3. current project policy and status;
4. role-specific official source and active checkpoint;
5. historical logs and generated documents.

Generated prose and PDFs are outputs, not sources of truth.

## Compact job packet

Discovery should hand the application worker a bounded object containing the official URL, requisition ID, role facts, screening result, evidence references, unresolved fields, and duplicate key. See `templates/job_packet.example.json`.

Do not pass entire model transcripts, browsing traces, every prior resume, or unrelated candidate folders.

## Field decision contract

A safe browser loop has five distinct stages:

```text
extract exact label/options/help text
→ classify into a small schema
→ validate schema
→ evaluate deterministic policy
→ act only on an explicit allow result
```

Recommended outcomes:

- `AUTO_FILL`: exact approved rule and value source exist;
- `SKIP_OPTIONAL`: policy explicitly permits omission;
- `NEED_HUMAN`: answer or human-only action is required;
- `BLOCK`: role or field must not proceed;
- `MANUAL_CHECK`: tooling or evidence is unreliable.

The model never upgrades itself from `NEED_HUMAN` to `AUTO_FILL`.

## Checkpoint before handoff

Before asking the applicant to intervene, record only:

- stable job key and official URL;
- current ATS step;
- exact blocking label and available options;
- why policy stopped;
- completed non-sensitive steps;
- what the human must do;
- how the worker will verify and resume.

After the human action, re-observe the current page. Do not assume the page, session, or field state is unchanged.

## Submission evidence

Mark `SUBMITTED` only after one of the following is captured:

- an ATS confirmation page clearly tied to the current role;
- a submission receipt or confirmation identifier;
- a successfully sent, authorized employer email when email is the submission channel.

An uploaded resume, disabled button, generated file, or ambiguous navigation is not sufficient.

## One-fallback recovery rule

When a tool action fails:

1. refresh the current state and confirm whether the first action actually occurred;
2. try one materially different safe fallback;
3. if the result remains uncertain, checkpoint as `MANUAL_CHECK` and stop acting on that role;
4. continue unrelated safe work.

Never click Submit twice unless the first attempt is positively known to have failed.

## Durable write-back

At every completed or paused role, update:

- application log: verified lifecycle result and evidence reference;
- current console: only active blockers, metrics, and one next action;
- manual queue: unresolved human tasks only;
- account and ATS registries: non-secret state changes;
- run ledger: operating cost and attribution;
- decision log: new durable policy decisions or exceptions.

Move resolved queue items to history instead of leaving them in the current view.
