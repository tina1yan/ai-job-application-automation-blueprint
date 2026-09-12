# Security and privacy policy

This repository is designed to remain free of real applicant and employer-confidential data.

## Never commit

- names, personal email addresses, phone numbers, home addresses, or government identifiers;
- resumes, cover letters, application receipts, application histories, or assessment content;
- passwords, API keys, tokens, cookies, MFA seeds, verification codes, or recovery codes;
- protected self-identification answers;
- browser profiles, screenshots, raw page captures, or debug logs from live applications;
- employer-confidential documents or internal job-system data.

Use aliases and the reserved `.invalid` domain in examples. Keep production facts and secrets in access-controlled systems outside the repository.

## Automation boundary

A language model's interpretation is not authorization to type, click, or submit. Place a deterministic, fail-closed policy check between classification and browser action. Unknown, malformed, conflicting, or risky inputs should result in `NEED_HUMAN`, `BLOCK`, or `SKIP`.

Never bypass CAPTCHA, MFA, anti-bot controls, identity checks, electronic signatures, assessments, payments, or legal attestations.

## Reporting a vulnerability

Please report security issues privately through GitHub's security advisory feature if enabled. Do not include live applicant data, credentials, or exploit data from a system you do not own.
