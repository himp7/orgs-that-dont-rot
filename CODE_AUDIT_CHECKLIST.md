# Code Audit Checklist

For auditing an org you've *inherited* or one that's been running a while — finding the debt that's already there. Work through it section by section; log findings as tech-debt user stories (see `templates/tech-debt-user-story.md`) so they compete for backlog priority instead of living in someone's head.

Run [Salesforce Code Analyzer v5](audits/CODE_ANALYZER_QUICKSTART.md) first — it'll automate a good chunk of this. Use this checklist for the judgment calls the scanner can't make.

## Triggers and Apex 

- [ ] How many triggers per object? (More than one = execution-order risk.)
- [ ] Does trigger logic live in the trigger, or in a handler class?
- [ ] Any recursion guards? Any evidence of recursive-trigger incidents in logs?
- [ ] SOQL or DML inside loops anywhere? (Code Analyzer flags these.)
- [ ] Longest Apex class / trigger by line count — is there an 800-line monster?
- [ ] Test classes: real assertions, or coverage-padding? Any `SeeAllData=true`?

## Hardcoded values

- [ ] Grep for record type IDs (`012`), profile IDs (`00e`), user IDs (`005`), org-specific URLs.
- [ ] Hardcoded usernames, emails, or environment endpoints in code.
- [ ] Magic strings that should be Custom Metadata or Custom Labels.

## Data model

- [ ] Any object with an unusually high field count? (Overloaded-object smell.)
- [ ] Fields whose meaning depends on record context (a field doing three jobs).
- [ ] Orphaned fields — created, never populated, never removed.
- [ ] Reports or list views that quietly rely on ambiguous fields.

## Automation sprawl

- [ ] Count automations per object across Flows, Apex triggers, and any legacy Process Builder / Workflow.
- [ ] Is execution order defined and understood, or accidental?
- [ ] Same logic implemented twice in different tools?

## Security and access

- [ ] Users with System Administrator who don't need it.
- [ ] Over-broad profiles where permission sets would scope better.
- [ ] Sharing settings that grant more than the business requires.
- [ ] CRUD/FLS enforcement in Apex that runs in system context.

## AI-generated code (new)

- [ ] Can the team identify which code was AI-assisted? Is it reviewed to the same bar?
- [ ] Spot-check AI-authored PRs for the SOQL-in-loop pattern and swallowed edge cases.
- [ ] Is there a deterministic quality gate (Code Analyzer / review) on *every* change, human or AI?

---

For each box you can't check, don't fix it in place on the spot — log it as a user story with an impact estimate, so it gets prioritized against everything else competing for the team's time.
