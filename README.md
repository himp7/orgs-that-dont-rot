# Orgs That Don't Rot 🏎️

> **A race car is fastest on lap 1. That's the problem.**

Preventative resources for keeping Salesforce orgs maintainable — the companion repo to the talk **"Tech Debt Starts on Day One: Building Salesforce Orgs That Don't Rot"** (Texas Dreamin' 2026).

![Salesforce](https://img.shields.io/badge/Salesforce-00A1E0?logo=salesforce&logoColor=white)
![Code Analyzer](https://img.shields.io/badge/Code%20Analyzer-v5-B30809)
![License: MIT](https://img.shields.io/badge/License-MIT-0591CD.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

---

Tech debt isn't from bad developers. It's good ones making reasonable decisions under pressure — and the debt gets baked in on day one, when everything still feels fast. Like tyre degradation, you don't feel it accrue; then you're two seconds off the pace and pitting under pressure.

This repo is the toolkit for making the *other* decision: the small, deliberate cost now — the planned pit stop — instead of the catastrophic one later.

## 🚦 Start here

**Building something today?** → [`DEPLOYMENT_CHECKLIST.md`](DEPLOYMENT_CHECKLIST.md) — the two gates, before you build and before you ship.

**Inherited an org and want to know how bad it is?** → [`audits/CODE_AUDIT_CHECKLIST.md`](audits/CODE_AUDIT_CHECKLIST.md) + [`audits/CODE_ANALYZER_QUICKSTART.md`](audits/CODE_ANALYZER_QUICKSTART.md).

**Reviewing a PR?** → [`templates/CODE_REVIEW_MASTER_SHEET.csv`](templates/CODE_REVIEW_MASTER_SHEET.csv) — 60 checks across 12 sections.

**Using an AI coding assistant?** → [`AGENTS.md`](AGENTS.md) — drop-in guardrails so it stops generating the anti-patterns.

## 📂 What's here

| Resource | What it's for |
|---|---|
| [`DEPLOYMENT_CHECKLIST.md`](DEPLOYMENT_CHECKLIST.md) | The two-gate checklist: before you build, before you ship. Print it, pin it. |
| [`audits/CODE_AUDIT_CHECKLIST.md`](audits/CODE_AUDIT_CHECKLIST.md) | A structured audit for an existing org — find the debt you already have. |
| [`audits/CODE_ANALYZER_QUICKSTART.md`](audits/CODE_ANALYZER_QUICKSTART.md) | Get Salesforce Code Analyzer v5 running in CI in ten minutes. |
| [`templates/CODE_REVIEW_MASTER_SHEET.csv`](templates/CODE_REVIEW_MASTER_SHEET.csv) | 60-check review sheet — bulkification, security, triggers, tests, async, AI code. Opens in Sheets/Excel. |
| [`templates/CODE_REVIEW_MASTER_SHEET_README.md`](templates/CODE_REVIEW_MASTER_SHEET_README.md) | How to use the sheet — columns, severities, the gate. |
| [`templates/tech-debt-user-story.md`](templates/tech-debt-user-story.md) | Make debt visible to the backlog so it competes for priority — costed as a number. |
| [`AGENTS.md`](AGENTS.md) | AI-assistant guardrails — steer any coding assistant toward the right patterns. |
| [`AI_ASSISTANT_SETUP.md`](AI_ASSISTANT_SETUP.md) | How to wire `AGENTS.md` into Claude Code, Cursor, Copilot, and others. |
| [`ci/`](ci/) | A ready-to-use GitHub Action running Code Analyzer on every PR. |

## 🏁 The five shortcuts this repo helps you avoid

Each one is a *reasonable* decision under pressure — that's why they happen. The fix is the call you make instead, at the same moment.

| # | The shortcut | The call you make instead |
|---|---|---|
| 1 | **Hardcoded IDs** | Resolve record types by developer name (`getRecordTypeInfosByDeveloperName()`); config in Custom Metadata / Labels. |
| 2 | **The 800-line trigger** | One trigger per object, delegating to a handler class, with a recursion guard. |
| 3 | **The overloaded object** | A field is a data-model decision, not a text-box decision. Model the entity. |
| 4 | **Flow vs. Apex by default** | Pick the tool on purpose, with an org-wide decision matrix. |
| 5 | **"System Admin for now"** | Least privilege is the first call — min-access profile + permission set groups. |

## 🤖 And the sixth, new for 2026: AI slop

AI assistants generate all five of the shortcuts above — instantly, and it looks clean. It reproduces the intuitive-but-wrong pattern (SOQL in a loop, most commonly) because that's what's most common in its training data. It passes the demo, then hits the governor limit on real data.

**Treat AI output as a first draft, not a deploy.** The checklists here are the review gate between machine-speed generation and your production org. [`AGENTS.md`](AGENTS.md) steers the assistant up front; Salesforce Code Analyzer v5 catches what slips through — and even integrates with Agentforce Vibes to suggest fixes for common violations.

## ⚡ Quick start

```bash
# Clone
git clone https://github.com/himp7/orgs-that-dont-rot.git

# Run Salesforce Code Analyzer v5 on your project
sf plugins install code-analyzer
sf code-analyzer run --workspace force-app --output-file results.html

# Wire the AI guardrails into your assistant (example: Claude Code)
cp AGENTS.md CLAUDE.md
```

See [`AI_ASSISTANT_SETUP.md`](AI_ASSISTANT_SETUP.md) for Cursor, Copilot, and others.

## 🎤 The talk

Presented at **Texas Dreamin' 2026** by [Himanshu Pandey](https://www.linkedin.com/in/himp7) — Specialist Architect, Accenture.

> Good orgs aren't built by better developers. They're built by better decisions — starting on lap 1.

## 🤝 Contributing

Found a shortcut that haunts you, or a check worth adding? PRs and issues welcome. This is meant to be a living toolkit — fork it, adapt it for your team's standards, and send back anything that would help others.

## 📄 License

[MIT](LICENSE) — use it, fork it, adapt it for your team. Attribution appreciated but not required.
