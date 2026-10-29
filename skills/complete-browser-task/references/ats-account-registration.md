# ATS account entry, registration, and verification

Use this reference when an authorized job application or other website workflow reaches a login screen, browser password suggestion, account creation, or ordinary sign-up email verification. **This is an execution protocol, not permission to access new accounts, defeat security controls, or submit an application.**

## Account identity comes before the browser click

Compute an employer-scoped account key from the **official application URL**, employer identity, ATS platform, and **tenant/organization identifier**. Consult the authorized local account registry and current browser context first. A generic Workday domain or a familiar email address does not prove that a saved login belongs to this employer.

Do not put real applicant identifiers, saved passwords, email messages, cookies, or session material in skill text, public repos, prompts, logs, screenshots, or exported checkpoints.

## Decision sequence

1. **Check session and existing registry.** If this exact tenant already has a verified signed-in session, reuse it. If a known account is recorded, follow its authorized sign-in route; do not create a second one.
2. **Inspect browser-managed saved-login suggestions.** Browser autofill and password-manager overlays can display credentials previously used for another employer. Match the current employer/tenant and registry before selecting a suggestion. If it matches an approved account, use the browser's normal UI to choose it, then make at most **one bounded sign-in attempt**.
3. **Do not fish through other saved accounts.** Reject suggestions from other employers/tenants even if the ATS branding, domain, or username appears similar. Never extract, enumerate, copy, display, or transfer password-manager secrets or cookies to the agent. If a browser-native overlay cannot be reliably clicked by the chosen tool, request user handoff or an allowed provider-native mechanism instead of blind coordinate retries.
4. **Resolve login outcome.** A confirmed sign-in finishes this phase. A rejected login is not automatically proof that no account exists. Inspect the site's message, tenant URL, account registry, and observed page state. Do not repeatedly guess credentials, trigger lockouts, or spam reset requests.
5. **Choose registration only when appropriate.** If no matching account exists and the site offers an authorized Create Account / Sign Up path, register using approved non-secret profile facts. If an existing account might be present, use the site's normal recovery or user-handoff path before creating a duplicate. Reuse any authorized employer-specific account across that employer's vacancies.
6. **Verify registration, separately.** A Create Account click is not the success criterion. Confirm the account-created state, then any required ordinary sign-up verification through an explicitly authorized, narrow employer-email matcher or user handoff. Mark VERIFIED only with site-side evidence. MFA, CAPTCHA, identity/e-signature attestation, login OTP, and password-reset or recovery codes remain protected handoffs; do not bypass them.
7. **Checkpoint the exact stage.** Record the employer-scoped tenant key (non-secret), action, observable result, stage (UNKNOWN / LOGIN_ATTEMPTED / SIGNED_IN / REGISTERED_UNVERIFIED / VERIFIED / NEED_HUMAN), and next safe step. Save no secrets or full applicant fields. Once the site is verified, continue the separately authorized application steps.

## Workday cross-employer trap

Workday careers pages often look alike. A saved login for fictional employer A may be offered on fictional employer B's page. **Do not trust the first autofill suggestion just because it is visible.** Confirm the exact tenant and account registry match. One authorized sign-in attempt is enough; a mismatch or failure must redirect to the normal employer-specific account discovery, recovery, or registration decision.

## Cost-aware execution

- **First:** deterministic browser controls (Playwright, accessible DOM locators, existing form recipes) and approved JSON fact/answer lookups. No model reasoning for known field labels and values.
- **Then:** optionally a local UI vision executor such as UI-TARS for a visual-only control, after observing the live page. A local vision model can still be wrong; verify what changed.
- **Only when necessary:** a reasoning model for genuinely unknown wording, page classification, or exceptional forms. It cannot invent personal facts or authorize protected actions.
- **Optional last resort:** a quota-based hosted tool such as TinyFish for a bounded, permitted task. Never make the flow dependent on having credits, and do not switch tools to evade CAPTCHA, denial, or quota enforcement.

## Home test matrix (non-production or authorized sandbox first)

| Scenario | Expected result |
| --- | --- |
| Exact employer account and matching saved-login suggestion | One permitted sign-in attempt; verify resulting session. |
| Saved Workday credential belongs to a different employer | Ignore it. No credential leak or cross-tenant login. |
| New employer with no known account | Visit Create Account; fill approved fields; checkpoint if any protected challenge appears. |
| Login fails but account may already exist | Use normal recovery / user handoff. Do not blindly duplicate. |
| Ordinary verification email arrives for current registration | Act only if a narrowly authorized matcher confirms employer, identity and timing; otherwise handoff. |
| Native password-manager overlay cannot be clicked | Bounded handoff; no repeated guessing coordinates. |
| CAPTCHA, MFA, identity check, or terms outside routine scope | Stop this account phase and preserve a redacted checkpoint. |

**Evidence rule:** logged in, account created, email verified, and job application submitted are four different milestones. Never conflate them.
