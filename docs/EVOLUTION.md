# AI Job Auto Apply — DSF4.1 大肥鱼：Evolution & Lessons 🐟

> Public, sanitized architecture history. This is **not** the original executable DeepSeek/BigFish runtime and **not** the private active job-application system.

## Why this page exists

A sequence of attempts taught an important lesson: the difficulty of reliable job applications is not mainly writing cover letters. It is account state, employer-specific ATS tenants, verified personal facts, recoverable workflows, human interrupts, and honest outcome accounting.

The following are **historical design generations**, not separate releases or runnable folders in this repository. They are described from the project's owner experience. An experiment should not be called production-ready merely because a component or fixture passed.

| Generation | Main approach | The useful part | What was not solved |
|---|---|---|---|
| V1 — DSF4.1 / BigFish | DeepSeek-orchestrated three-agent approach; Playwright added later; attempted token/cost constraints | Role separation, workflow planning, explicit cost measurement | Coordinating agents and cost limits did not yield a stable automated job-registration-and-application path |
| V2 — Codex assisted | Powerful model conducts end-to-end browser work | Flexible reasoning and substantial real application progress | Repetitive form clicks were expensive in model attention, and new accounts required frequent human handoffs |
| V3 — Scheduled Codex | Scheduled workstation workflow, experimenting with Sol and Terra | Scheduling, checkpoints, logging and the ability to resume | Changing models did not resolve ATS sign-up, login and verification bottlenecks |
| Next — modular runtime (private, not published here) | FactBook/JSON + deterministic form driver + isolated auth/visual module + exception model | Reuse known facts, reduce model usage, separate failure handling from business judgment | End-to-end unattended Workday production behavior has not been independently verified |

## Reusable system design

1. **Canonical FactBook:** verified personal/professional facts have an owner, provenance and revision date. Generate structured JSON once, then prefill routine fields through deterministic code.
2. **Deterministic first:** use selectors, validation, account-state registry and Playwright for known paths; allocate reasoning to unfamiliar wording and genuine conflicts.
3. **Identity and tenant boundaries:** a saved browser credential for one employer's Workday tenant is not automatically valid for another employer. Exact tenant/account matching is necessary before reuse. If login fails, inspect cause before choosing ordinary recovery or account creation.
4. **Local visual helper:** a local UI model can propose a click on tricky controls, but the host must check the actual target, session, permission and outcome. The model is not an autonomous source of authority.
5. **Proof over claims:** a generated resume, clicked button or sent verification email is not submission evidence. Record a matching receipt/success state or leave the task unverified.
6. **Failure playbook:** capture sanitized site state, failure cause, approved fix, test date and scope. A first success is not universal proof.
7. **Track the honest cost:** count model tokens, human time, dead ends and all attempts; normalize by confirmed submissions and eventually responses/interviews.
8. **Keep privacy boundaries:** credentials, resume originals, account email contents, personal facts, application logs, screenshots and employer-specific private data are outside this public repository.

## Where the other pieces belong

- **This GitHub repository:** publicly shareable, generalized blueprint and starter templates.
- **Private knowledge store:** canonical career facts, the application tracker, version map, lessons learned and verification records.
- **Current private runtime:** executable code and model-routing configuration. It does not become a public release merely because a historical blueprint exists.
- **ATS authorization component:** separate host-scoped registration/login helper. Its private local implementation is not included in this repository.
- **TinyFish:** used in a **separate website-deployment/Google Search Console** workflow. It is not the job-account registration model.

The public [Complete Browser Task skill](../skills/complete-browser-task/SKILL.md) is a **general workflow guide**, not an installer for private ATS accounts or a preconfigured automated job applicant.

## Versioning rule

A **repository** is a project boundary. A **branch** is a change under test. A **release/tag** is a tested snapshot. A model swap (Sol/Terra, for example) is usually a configuration or experiment change, not automatically a new major release.

Preserve older experiments and identify what has actually been verified. Never re-label an untested private runtime as a working public tool.
