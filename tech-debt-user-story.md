# Tech Debt User Story Template

Debt that lives in a developer's head never gets fixed — it can't compete for priority against features that have a story and an estimate. This template makes debt *visible and costed* so it competes fairly. Copy one per item into your backlog tool.

The trick is framing: don't write "refactor the trigger." Write it as a risk with a cost, in the language the person prioritizing the backlog actually uses.

---

## Title

`[TECH DEBT] <short description>` — e.g. `[TECH DEBT] AccountTrigger has SOQL inside a loop`

## Story

> **As** the team maintaining <org / object / feature>,
> **we have** <the shortcut / the current state>,
> **which will** <the haunt — what breaks, when, and for whom>,
> **so we should** <the prevention — the call we make instead>.

## The three parts (from the talk)

- **Trigger** (why the shortcut was reasonable): _____
- **Shortcut** (what's there now): _____
- **Haunt** (how and when it comes back): _____

## Impact — make it a number, not an opinion

- **What fails, and at what scale?** e.g. "Fails on any bulk update of 100+ Accounts — Data Loader, API jobs."
- **Blast radius:** who/what is affected when it triggers?
- **Likelihood / timeline:** already happening / next data load / next record-type change / eventually.
- **Cost of the haunt:** support hours, downtime, failed deploys, rework.
- **Cost to prevent now:** _____ (usually far smaller — that's the argument.)

## Definition of done

- [ ] Prevention implemented (see `DEPLOYMENT_CHECKLIST.md`)
- [ ] Covered by a test that proves the fix (bulk where relevant)
- [ ] Passes Code Analyzer with no new high-severity violations
- [ ] Reviewed against the master sheet

## Links

- Related PR / class / flow: _____
- Code Analyzer finding (if any): _____

---

*Argue from the pit wall, not the driver's seat. "We should do it right" loses. "This fails at 100 records and costs us a Saturday" wins.*
