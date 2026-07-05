# Code Review Master Sheet

A comprehensive Salesforce review instrument — 60 checks across 12 sections. Import `CODE_REVIEW_MASTER_SHEET.csv` into Google Sheets or Excel and work top to bottom, or filter to what a given PR touches. 

## How to use it

- **Per PR:** filter to the sections the change touches (e.g. a trigger PR → Bulkification, Triggers & Handlers, Security, Tests, AI-Generated if applicable). Mark each row Pass / Fail / N/A in the Status column.
- **As a team standard:** agree which severities are blocking. A common gate: **Critical must pass; High needs a logged tech-debt story if deferred; Medium/Low are advisory.**
- **With automation:** the *Auto-detected* column tells you which checks Salesforce Code Analyzer catches, so reviewers spend their attention on the judgment calls the scanner can't make.

## Columns

| Column | Meaning |
|---|---|
| **Section** | Grouping (Bulkification, Security, Tests, etc.) |
| **Check** | The specific thing to verify |
| **What good looks like** | The passing state, in one line |
| **Severity** | Critical / High / Medium / Low — set your own gate |
| **Auto-detected** | Yes / Partial / No — does Code Analyzer catch it? |
| **PMD / Analyzer rule** | The specific rule name, where one exists |
| **Reference** | Where the guidance comes from |
| **Status** | You fill in: Pass / Fail / N/A |
| **Reviewer notes** | You fill in |

## Severity guidance

- **Critical** — will break in production or open a security hole. Block the merge.
- **High** — real risk or significant debt. Fix, or log a tech-debt story before merging.
- **Medium** — maintainability and correctness; address in normal course.
- **Low** — hygiene and consistency; nice to fix, don't block on it.

## Notes on currency (2026)

A few checks reflect recent Salesforce changes worth calling out:

- **`WITH USER_MODE`** is the current way to enforce CRUD/FLS in SOQL/SOSL, and **`WITH SECURITY_ENFORCED` is being retired** — `USER_MODE` is its successor. DML enforces user permissions with the `as user` keyword.
- **Least privilege** now means the *minimum-access profile + permission set groups* model; Salesforce is steering teams away from cloning profiles.
- **AI-generated code** gets its own section — the same anti-patterns (especially SOQL-in-loops) that AI reproduces by default need explicit verification, and Code Analyzer v5 can suggest fixes for many via Agentforce Vibes.

Rules and rule names track Salesforce Code Analyzer v5 / PMD. Verify exact rule selectors against your installed version, since Salesforce ships updates frequently.
