# Salesforce Code Analyzer v5 — Quick Start

Salesforce's own static analysis tool. Free, official, and the current version — **v4 was retired in August 2025**, so make sure you're on v5. It bundles multiple engines (PMD for Apex, ESLint for LWC/JS, RetireJS for outdated libraries, Regex, and the Flow Scanner) under one CLI, with 500+ built-in rules covering Apex, Visualforce, Flows, and Lightning components.

## Install

Requires the Salesforce CLI (`sf`).

```bash
sf plugins install code-analyzer
```

## Run a scan

From your project root:

```bash
# Scan everything with the recommended rules
sf code-analyzer run --workspace .
 
# Write an HTML report you can browse (search, grouping, severity)
sf code-analyzer run --workspace . --output-file results.html

# Scan just Apex, just the high-severity stuff
sf code-analyzer run --rule-selector Recommended:pmd:Apex --workspace force-app
```

Outputs support csv, xml, json, sarif, and html.

## List and select rules

```bash
# See every available rule
sf code-analyzer rules

# See the Apex security and error-prone rules
sf code-analyzer rules --rule-selector Recommended:pmd:Security:Apex
```

Rules carry tags and severities, so you can gate on, say, only high-severity security violations while you work down the rest as tech-debt stories.

## Fixing AI-generated violations

Code Analyzer v5 integrates with Agentforce Vibes — for a set of PMD violations it can suggest a fix you accept or reject. Handy when the debt was AI-authored in the first place. See Salesforce's "Fix Your Code Using Agentforce Vibes" docs.

## A note on legacy orgs

Code Analyzer scans your *whole* codebase, not just the diff — so on an org with years of accumulated debt, the first run will surface a lot. Don't try to fix it all at once. Gate new code on "no *new* high-severity violations," and burn down the backlog as prioritized stories. (Some commercial tools distinguish new debt from old automatically; the free tool doesn't yet.)

## Docs

- Overview: https://developer.salesforce.com/docs/platform/salesforce-code-analyzer/guide/code-analyzer.html
- Command reference and release notes are linked from that overview page.
