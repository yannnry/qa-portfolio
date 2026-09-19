# Case Study: CBT Center — Instructor & Student Testing

## Objective

Validate the CBT Center module across both instructor and student-facing views, covering the dashboard, module list, and lesson player, including video playback and watch-time compliance tracking. The platform is used for regulated aviation training, so completion and watch-time data has to be trustworthy, not just functional on the surface.

## Scope

* Instructor dashboard and CBT Center landing page
* Subject module list (publish/unpublish actions)
* Module and lesson player view
* Student CBT Center dashboard
* Student lesson player, including the anti-skip / watch-time mechanism

## Method

Manual exploratory testing combined with structured screenshot review and live interaction testing. Rather than working from a fixed script, each screen was tested against what a real instructor or cadet would actually do with it, then cross-checked against expected platform behavior.

## Test Design

* Functional walk-through of publish/unpublish actions under different selection states (all-draft, all-published, mixed)
* Visual consistency check across instructor and student views, since the two are meant to render identically
* Boundary case: zero-progress state on dashboard charts
* Exploratory pass on the video player, specifically testing whether the in-app watch-time tracking could be bypassed by leaving the embedded player

## Findings

Nine findings were logged in the full audit; the five below carry this case study.

| ID | Finding | Type | Severity | Priority |
|---|---|---|---|---|
| SEC-01 | Lesson videos embedded as standard third-party player iframes allow the raw video URL to be extracted, bypassing in-app watch-time tracking | Security Risk | Major | High |
| BUG-02 | Bulk publish/unpublish actions do not check the status of selected items, allowing redundant or ambiguous batch actions | Bug | Minor | Medium |
| A11Y-01 | Inactive sidebar navigation text fails WCAG AA contrast in the lesson view | Accessibility | Minor | Medium |
| A11Y-02 | Secondary metadata text on the student dashboard falls below WCAG AA contrast | Accessibility | Minor | Medium |
| UX-04 | Anti-skip watch-time mechanism works correctly inside the app (positive finding), but its protection stops at the app boundary | UX Improvement | Cosmetic | Low |

### SEC-01 in detail

The lesson player embeds training videos using a standard third-party iframe with native branding controls left active. Any student can extract the raw video URL and watch it outside the platform entirely, which does two things at once: it exposes proprietary training content outside an authenticated session, and it defeats the in-app anti-skip mechanism, since none of that external viewing gets reported back. For a platform tracking regulated training hours, the second consequence is the one that matters most — a student could technically satisfy a watch-time requirement without the platform ever recording it.

This finding connects directly to UX-04. The anti-skip mechanism itself works as intended: skipping ahead inside the app triggers a clear warning and a one-click recovery option, and progress tracking is accurate. It just has no reach past the app's own boundary, which is what makes SEC-01 a bypass of the *system*, not a flaw in that one mechanism.

**Recommended fix**, in order of effort:

1. Strip native player controls and build a custom control bar via the platform's IFrame API — reduces the surface for casual link extraction without a platform change.
2. Add a visible compliance notice near the player stating that watch time is only recorded inside the app.
3. Longer term, migrate to a domain-restricted video host so playback requires an authenticated session on the platform's own domain.

## Verification

This case study documents findings as reported; verification of the CSRF-style bypass and the fix status is intentionally out of scope for this public write-up, since that depends on post-fix retesting against the live environment.

## What This Case Study Shows

Reading a defect in isolation ("videos can be extracted") understates the actual risk. Tracing it against a working feature (the anti-skip mechanism) is what surfaces the real impact — a compliance gap, not just a content-protection gap. That connection is the reason this case study leads with SEC-01 rather than treating it as one line in a findings table.
