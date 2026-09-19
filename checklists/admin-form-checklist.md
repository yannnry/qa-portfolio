# Admin Form Checklist

Scoped checklist for admin-side data-entry forms, built from two recurring scenario categories: status-dependent bulk actions and unintended data loss. Run this against any new or modified admin form before it ships.

## Bulk / Batch Actions (from SCN-01)

- [ ] Are bulk action buttons disabled when the current selection makes the action meaningless (e.g. "Unpublish" when everything selected is already a draft)?
- [ ] Does a mixed-status selection produce either a clear disabled state with an explanation, or safe, idempotent behavior?
- [ ] Is the zero-selection state handled (buttons inactive, no error thrown)?

## Form Persistence (from SCN-03)

- [ ] Does a page refresh mid-entry trigger a warning, or does it silently discard data?
- [ ] Does browser back navigation behave the same way as a refresh?
- [ ] Does closing the tab trigger a `beforeunload` prompt when unsaved changes exist?
- [ ] Is there no prompt when navigating away with no unsaved changes (false positives are as bad as missing warnings)?

## Input Validation

- [ ] Are duplicate values rejected where uniqueness matters, including case and whitespace variants?
- [ ] Does every field enforce a sane maximum length, with the validation error mapped to the correct field?
- [ ] Is whitespace trimmed server-side before a required-field check runs?

## Feedback

- [ ] Is submission feedback (success/error) visible regardless of scroll position, not just at the top of the page?
- [ ] Does the submit action show a loading/disabled state so a slow response is not mistaken for a failed submit?

**Traceability:** Items in this checklist trace to `SCN-01`, `SCN-03` (`test-scenarios/scenarios.md`) and to findings `BUG-02`, `BUG-04` documented in `case-studies/`.
