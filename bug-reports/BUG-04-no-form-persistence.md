# BUG-04 — No Form-State Persistence on Refresh, Back Navigation, or Tab Close

**Type:** Bug
**Severity:** Major
**Priority:** High
**Reproducibility:** Always

## Location

Admin — Add Question form

## Environment

Production build, desktop browser

## Description

There is no autosave, draft-recovery, or unsaved-changes warning on the Add Question form. Refreshing the page, navigating back, or closing the tab while a question is partially filled out discards everything entered, silently.

## Steps to Reproduce

1. Open the Add Question form.
2. Fill in the question text and at least one answer option.
3. Refresh the page (or navigate back, or close the tab).
4. Return to the form.

## Expected Behavior

Either the form should persist in-progress data automatically, or the browser should prompt a confirmation before discarding unsaved changes.

## Actual Behavior

All entered data is lost immediately, with no prompt and no way to recover it. No `beforeunload` warning is triggered.

## Impact

For a form used to author exam content, an accidental refresh mid-entry means re-typing a full question and its answer options from scratch. Combined with other validation gaps found in the same audit (duplicate answers accepted without warning, misdirected validation errors), this points to a form where the error-prevention and recovery paths were not built to the same standard as the core submission flow.

## Recommended Fix

* Add debounce-based autosave to local storage or a backend draft endpoint while the admin types.
* Add a `beforeunload` confirmation prompt when the form has unsaved changes.
* On page load, detect and offer to restore any existing draft.

## Status

Open — reported, fix not yet verified.
