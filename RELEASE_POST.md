# Launch post — v0.1.0

I made my AI job-application workflow public 😭🤖

It is not another “spray 500 applications while you sleep” bot. It is a privacy-first blueprint for the unglamorous parts that decide whether automation is actually trustworthy: fact provenance, ATS/account registries, `NEED HUMAN` blockers, model routing, submission evidence, and honest cost-per-confirmed-submission metrics.

The repo contains sanitized architecture docs and starter templates—no resumes, credentials, real application history, or employer data.

I am sharing v0.1 because I would genuinely love feedback: what breaks, what is too complicated, and what would make this safer or more useful? 😂🚀

**Repository description:** A privacy-first, human-in-the-loop blueprint for AI-assisted job applications: ATS/account registries, hard blockers, model routing, and honest cost-per-confirmed-submission metrics. 🤖📮

## Update — 2026-10-29: UI-TARS and the Workday login trap

> UI-TARS 怎么这么好用，怎么没多少人讨论？😂 我在自己的 RTX 4090 上测试了求职网站的账号注册流程，真的有种把重复点击工作交出去的快乐。
>
> 但是我发现一个很真实的坑：不同公司的 Workday 账号看起来很像，浏览器却会联想出另一家公司的保存密码。正确做法不是疯狂试密码，而是先识别当前公司/tenant，能复用正确账号就登录，不匹配就走当前公司的注册或正常找回流程。
>
> 我把这条规则和注册验证、未知表单问题的知识库机制整理进了公开的 [Complete Browser Task skill](skills/complete-browser-task/SKILL.md)。已知资料尽量用 Playwright 直接预填；复杂页面交给本地 UI-TARS；真正需要判断的新问题才调用模型。**TinyFish 是我另一条网站部署 / Google Search Console 工作流，不负责这里的求职注册。**
>
> 这还是一个持续测试中的方案：本地单次成功不代表所有 Workday 网站都跑通，回家会继续做更严格的测试。欢迎讨论你们遇到过的 ATS 登录坑。🤖

**English short version:** Local UI-TARS on an RTX 4090 made an account-registration test feel surprisingly smooth. The catch? Workday-style career sites can trigger saved-password suggestions for the wrong employer's tenant. I added employer-scoped login checks, bounded recovery/registration, and a contextual answer-bank protocol to my public [browser workflow skill](skills/complete-browser-task/SKILL.md). Playwright handles known fields; UI-TARS handles local visual UI; reasoning models handle genuinely unknown questions. This is a user-reported test, not a claim of production-grade universal automation. TinyFish belongs to a separate Search Console deployment workflow.
