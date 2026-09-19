# Test Cases — Form Data Persistence (derived from SCN-03)

Coverage here separates the *trigger* (what causes potential data loss) from the *expectation* (a warning should appear only when there is something to lose), since the original defect combined both a missing warning and no recovery path.

| Trigger | Represents |
|---|---|
| T1 — Page refresh mid-entry | Accidental reload |
| T2 — Browser back navigation mid-entry | Accidental navigation |
| T3 — Tab close mid-entry | Accidental close |
| T4 — Navigation away with no unsaved changes | Control case — should not prompt |

---

**TC-01 — Refresh mid-entry (T1)**

| Field | Value |
|---|---|
| Preconditions | Admin has started filling out the Add Question form with at least the question text entered |
| Steps | 1. Enter question text and at least one answer option.  2. Refresh the browser tab. |
| Expected Result | Either the entered data is restored automatically on reload, or a confirmation prompt appears before the refresh completes, giving the admin a chance to cancel. |

**TC-02 — Back navigation mid-entry (T2)**

| Field | Value |
|---|---|
| Preconditions | Admin has started filling out the form with unsaved data present |
| Steps | 1. Enter partial form data.  2. Trigger browser back navigation. |
| Expected Result | Same behavior as TC-01 — data is either preserved or an explicit confirmation is required before navigating away. |

**TC-03 — Tab close mid-entry (T3)**

| Field | Value |
|---|---|
| Preconditions | Admin has started filling out the form with unsaved data present |
| Steps | 1. Enter partial form data.  2. Attempt to close the browser tab. |
| Expected Result | A native `beforeunload` confirmation dialog appears, warning that unsaved changes will be lost. |

**TC-04 — Navigation away with no unsaved changes (T4)**

| Field | Value |
|---|---|
| Preconditions | Form is untouched, or was already submitted successfully |
| Steps | 1. With no unsaved data present, refresh, navigate back, or close the tab. |
| Expected Result | No confirmation prompt appears. This is a control case — a system that always warns regardless of actual state trains users to dismiss the warning without reading it. |

---

**Traceability:** TC-01 through TC-04 → SCN-03. TC-01 through TC-03 correspond directly to `BUG-04`, documented in both `bug-reports/BUG-04-no-form-persistence.md` and `case-studies/02-add-question-testing.md`.
