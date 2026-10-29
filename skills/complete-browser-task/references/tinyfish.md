# TinyFish task execution

Read the current tool schemas before calling; names and capabilities can change. Treat these as workflow guidance, not a replacement for live tool instructions.

## Select a profile

For a site requiring authentication, call `list_profiles` when available. Prefer a profile whose `signed_in_sites` covers the requested site, using the documented domain/provider matching rules. Pass its exact ID with `use_profile=true`. Do not assume the default profile is signed in or identifies the intended account.

If no appropriate sign-in is recorded, follow the returned setup/confirmation flow before starting. If a run reaches a login page, follow the documented expired-session recovery flow; do not loop the same automation. Use `start_profile_setup_session` or the supported profile page only when authorized by the current provider flow. Never collect credentials in chat. Use vault access only as documented and authorized, with the narrowest available scope.

## Compile a bounded goal

Use this template, replacing placeholders with grounded task data:

```text
Target: [exact website/resource]
Outcome: [one specific website task]
Existing state: [confirmed checkpoint, if any]
Inputs: [required nonsensitive facts]
Authorized actions: [navigate/fill/submit/change, scoped to target]
Preserve: [unrelated settings, records and privacy restrictions]
Success evidence: [exact resulting status/record to observe]
If an external prerequisite is needed: return the exact artifact and stop that stage.
If login, CAPTCHA, denied permission or quota occurs: report it and follow the supported handoff; do not circumvent.
Return: completed milestones, submission certainty, observed evidence, and precise blocker. Omit account identity and secrets.
```

Choose a reasonable step/time budget for the task. Do not silently authorize purchases, additional tasks, messages or unrelated account changes. Use structured output only if the current provider supports the requested schema.

## Run once, wait correctly

1. Call `run_web_automation` once for the bounded stage; retain its returned `run_id`/`runId` and provider context privately.
2. Call `wait_for_run` with that ID until completed, failed or cancelled, as directed by the provider. Do not substitute `get_run` or `list_runs` for polling when prohibited.
3. If `wait_for_run` errors, resume waiting on the same ID according to the provider instructions. If run creation times out without an ID, use the documented run-discovery recovery; do not start another run just to get an ID.
4. Inspect the terminal result. Separate observed site evidence from the agent's inference. A run labelled completed may still report an unverified property, a rejected form or a quota failure.
5. Start a new run only for a distinct next stage after the prior run is terminal, or after documented recovery establishes that retrying cannot duplicate a side effect.

When a metered run reports insufficient credits, relay the exact funding/upgrade path and ask only the required decision; do not silently substitute another tool when the provider requires otherwise. A low-balance notice is not itself an execution failure. Do not invent remaining credits or automatically top up.

## Cross-tool verification example

For an authorized site verification task:

- Stage A: select the appropriate Google session, add/select the exact URL-prefix property, and retrieve Google's complete HTML verification meta tag or exact file bytes.
- If download contents cannot be read, retrieve the displayed HTML tag instead. A filename alone is insufficient; never synthesize a verification token or file contents.
- Deploy the exact artifact through the authorized hosting connector, preserving existing verification artifacts and site identity. Confirm the public response contains it.
- Stage B: verify using the matching method in Search Console, submit the exact sitemap, and inspect/request indexing if supported and authorized.
- Record ownership success, submission acceptance, sitemap read status and indexing separately. “Submitted successfully” plus “Couldn't fetch” is partial success. “Quota Exceeded” during the live test is not a completed indexing request.

Do not hard-code real account IDs, profile IDs, domains, verification tokens, run IDs or personal names into this reusable skill.
