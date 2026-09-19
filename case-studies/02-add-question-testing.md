# Case Study: Admin — Add Question Page Testing

## Objective

Execute a full manual QA pass against the admin-side question-creation form, covering functional correctness, input validation, security posture, and performance, ahead of a broader admin-panel review.

## Scope

Admin — Add Question page: question text field, answer options, form submission, and success/error feedback.

## Method

A structured checklist run across eight categories — smoke, functional, UI/UX, validation and input, edge cases, security, performance, and a set of high-risk aggressive tests — rather than open-ended exploration. Checklist-based testing suits a form like this well, since the failure modes (missing validation, unbounded input, lost form state) are predictable enough to enumerate in advance, and a checklist forces every one of them to actually get checked instead of relying on what happens to come to mind during a session.

75 test cases were executed across the first seven categories. 12 aggressive/high-risk cases (DevTools manipulation, malformed payloads, session-hijacking simulation) were scoped but deliberately not run against the production environment, and are logged as follow-up work for a staging environment instead.

## Test Coverage Summary

| Category | Total | Passed | Failed | Other |
|---|---|---|---|---|
| Smoke Test | 10 | 10 | 0 | 0 |
| Functional | 6 | 5 | 0 | 1 |
| UI/UX | 12 | 8 | 4 | 0 |
| Validation & Input | 8 | 5 | 3 | 0 |
| Edge Cases | 7 | 3 | 3 | 1 |
| Security | 12 | 8 | 2 | 2 |
| Performance | 8 | 3 | 4 | 1 |
| High-Risk (not executed) | 12 | — | — | 12 |

"Other" covers cases deferred, in progress, or not applicable by design — a whitespace-validation case, for instance, was marked not applicable once the underlying behavior turned out to be a routing bug rather than a validation gap (see BUG-03 below).

## Findings

Fifteen findings were logged in the full audit; the six below carry this case study.

| ID | Finding | Type | Severity | Priority |
|---|---|---|---|---|
| SEC-01 | Missing CSRF token on state-changing form submission | Security Risk | Major | High |
| BUG-01 | Duplicate answer options accepted without validation | Bug | Major | High |
| BUG-04 | No form-state persistence — data lost on refresh, back navigation, or tab close | Bug | Major | High |
| BUG-03 | Whitespace-only question text is flagged against the wrong field | Bug | Minor | Medium |
| UX-01 | Submission feedback renders at the top of the page and is easy to miss on longer forms | UX Improvement | Minor | Medium |
| PERF-01 | Page load averages 5.41s against a 3s target | Performance | Minor | Medium |

### SEC-01 in detail

Network inspection during testing showed no CSRF token attached to the form's state-changing request — no token in the payload, none in the headers. Without one, the server has no way to confirm a submission actually originated from the platform's own UI, which opens the door to a request forged from an external page acting on behalf of an already-logged-in admin. This is the kind of gap that produces no visible symptom during normal use, which is exactly why it needs network-level inspection rather than UI testing to catch.

**Recommended fix**: enable CSRF middleware server-side to issue and validate a per-session token, and have the frontend attach it automatically to every state-changing request.

### BUG-04 in detail

There is no autosave and no `beforeunload` warning. An admin who accidentally refreshes, navigates back, or closes the tab mid-form loses everything typed, with zero warning beforehand. Paired with BUG-01 (duplicate answers silently accepted) and BUG-03 (validation errors pointing at the wrong field), this cluster tells a consistent story: the form's error-prevention and error-recovery paths were not built out to the same standard as its happy path.

**Recommended fix**: debounce-based autosave to local storage or a backend draft endpoint, plus a `beforeunload` confirmation prompt when unsaved changes exist.

## Verification

Documented as reported; fix verification is out of scope for this public write-up and depends on retesting against a build with the fixes applied.

## What This Case Study Shows

A checklist-based pass across eight categories caught issues that a single exploratory session likely would have missed — the CSRF gap in particular surfaced only because network inspection was part of the checklist, not because anything in the UI hinted at it. The category breakdown table also does double duty: it shows the CSRF and duplicate-answer findings as two failures out of many passes, not as flags of an unstable feature, which is a more accurate picture of where the actual risk sits.
