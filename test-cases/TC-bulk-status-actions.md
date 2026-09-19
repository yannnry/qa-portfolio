# Test Cases — Bulk Module Status Actions (derived from SCN-01)

Coverage is built around selection *state* rather than individual modules, since the defect this traces back to was a failure to check status before enabling an action. Four states are enumerated: single-status selections (two variants), a mixed-status selection, and the zero-selection baseline.

| State | Represents |
|---|---|
| S1 — All selected items Draft | Should allow Publish, block Unpublish |
| S2 — All selected items Published | Should allow Unpublish, block Publish |
| S3 — Mixed selection (Draft + Published) | Ambiguous case — should not silently allow either action without clarification |
| S4 — No items selected | Both actions should be inactive |

---

**TC-01 — Bulk action buttons with all-Draft selection (S1)**

| Field | Value |
|---|---|
| Preconditions | Subject module list has at least two modules in Draft status |
| Steps | 1. Select two Draft modules via checkbox.  2. Observe the "Publish Module" and "Unpublish Selected Modules" buttons. |
| Expected Result | "Publish Module" is active. "Unpublish Selected Modules" is disabled, since none of the selected items are currently published. |

**TC-02 — Bulk action buttons with all-Published selection (S2)**

| Field | Value |
|---|---|
| Preconditions | Subject module list has at least two modules in Published status |
| Steps | 1. Select two Published modules via checkbox.  2. Observe both action buttons. |
| Expected Result | "Unpublish Selected Modules" is active. "Publish Module" is disabled. |

**TC-03 — Bulk action buttons with mixed-status selection (S3)**

| Field | Value |
|---|---|
| Preconditions | Subject module list has at least one Draft and one Published module |
| Steps | 1. Select one Draft module and one Published module together.  2. Observe both action buttons. |
| Expected Result | Both buttons are either disabled with an explanatory tooltip (e.g. "Select only modules with the same status"), or the action proceeds against an idempotent backend that safely no-ops on already-correct items. Buttons must not simply remain active with undefined behavior. |

**TC-04 — Bulk action buttons with no selection (S4)**

| Field | Value |
|---|---|
| Preconditions | No modules are selected |
| Steps | 1. Observe the state of both action buttons with zero checkboxes checked. |
| Expected Result | Both "Publish Module" and "Unpublish Selected Modules" are disabled. |

---

**Traceability:** TC-01 through TC-04 → SCN-01. TC-01 and TC-02 correspond directly to the defect documented as `BUG-02` in `case-studies/01-cbt-center-testing.md` — S1 and S2 are the exact states where that defect was originally observed.
