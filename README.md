# Manual QA Software Testing Portfolio

Hi, I am **Joshua Ryan Altar**, a Manual QA Engineer with professional experience testing PSPACE, a live web-based EASA ATPL adaptive learning platform.

My work centers on validating software functionality, identifying and documenting defects, verifying fixes, and supporting release quality through structured and exploratory testing. I also evaluate user-facing behavior across usability, accessibility, and security-adjacent areas, and I compile findings into audit-style reports used directly by development teams for release planning.

## About This Portfolio

This repository contains selected examples of my testing work and my testing process, including:

* Test cases
* Test scenarios
* Bug reports
* Checklists
* Case studies (combining test planning, execution, and reporting)
* Exploratory and security-oriented testing examples

Some materials are **sanitized or independently recreated**. Screenshots, internal tickets, proprietary URLs, and confidential implementation details are excluded; the structure, reasoning, and findings reflect real testing work.

## Testing Methodology

I classify every finding using a fixed set of categories rather than an open-ended label, so severity and priority stay consistent across a full report instead of drifting case by case:

| Finding Type | Prefix | Meaning |
|---|---|---|
| Bug | `BUG-` | Reproducible defect in functionality, presentation, or interaction |
| Security Risk | `SEC-` | Security or content-protection risk backed by observed behavior |
| Performance | `PERF-` | Measurable or reproducible performance degradation |
| Accessibility | `A11Y-` | Accessibility barrier or WCAG-related issue |
| UX Improvement | `UX-` | Working feature that is confusing, inefficient, or inconsistent |
| Positive Finding | `POS-` | Working-as-intended behavior worth documenting |

Severity (impact) and priority (urgency to fix) are tracked as separate fields, not treated as interchangeable, and every finding distinguishes fact and direct observation from inference or hypothesis.

## Professional QA Experience

### PSPACE

**QA Engineer** · Feb 2025 – Present

EASA ATPL adaptive learning platform (pspace.app), serving as the primary QA checkpoint before releases.

Responsibilities include:

* Functional, regression, and exploratory testing
* Security-oriented testing (CSRF, CSP, auth bypass awareness)
* Accessibility auditing against WCAG AA
* Performance observation (page load, asset payload audits)
* Full-cycle QA audit reporting with severity/priority classification and root-cause hypotheses
* Defect verification and release validation
* Test case and test scenario design

## QA Case Studies

* Authentication and Account Testing
* 50-Question Free Trial Testing
* Question Bank Testing
* Security Testing (CSRF, deadline-bypass verification)
* Regression and Release Testing

See `case-studies/` for details.

## QA Artifacts

| Folder | Description |
|---|---|
| `test-cases/` | Structured test conditions, steps, and expected results |
| `bug-reports/` | Defect reports with reproduction steps, expected/actual results, severity, and priority |
| `test-scenarios/` | High-level testing conditions used to define functional coverage |
| `checklists/` | Reusable checks for common testing and regression activities |
| `case-studies/` | Combined test plan, execution, findings, and verification for a specific feature or flow |

## Tools & Technologies

**Testing**
Manual Testing · Functional Testing · Regression Testing · Exploratory Testing · Usability Testing · Security-Oriented Testing · Accessibility Auditing (WCAG AA)

**Tools**
Jira · TestRail · GitHub · Chrome DevTools (Network, Console, Coverage) · Microsoft Excel · Google Sheets · Postman

**Currently Learning**
ISTQB® Certified Tester Foundation Level (CTFL) v4.0.1 · API Testing · SQL and Database Testing · Test Automation Fundamentals

## Certifications & Training

* Software QA Manual Testing (Hands-On: Jira, TestRail, Excel) — MSTConnect Educational Consultancy, July 2026
* CS107: C++ Programming Language — Saylor.org Academy, April 2021
* Claude 101 — Anthropic Education, August 2026

## Resume

[View Resume](resume/Joshua-Altar-Resume.pdf) <!-- link to hosted PDF once available -->





## How These Folders Connect

The five folders are not independent collections — each documents the same underlying testing work from a different angle. To see the full thread, follow one finding across the repo:

1. **`test-scenarios/`** states the condition worth testing (e.g. `SCN-02` — answer option validation).
2. **`test-cases/`** derives specific, steppable cases from that scenario using equivalence partitioning.
3. Running those cases surfaces a defect, documented as a standalone report in **`bug-reports/`**.
4. **`case-studies/`** places that same defect in context — objective, execution, and the reasoning behind its severity and priority.
5. **`checklists/`** turns the lesson into something reusable, so the same class of defect gets caught earlier next release.

Start anywhere; each piece links back to the others.

## Contact

GitHub: [@yannnry](https://github.com/yannnry)
