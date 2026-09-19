# Test Scenarios

High-level conditions identified before test cases are written against them. Each scenario states *what* needs validation; the linked test cases (in `test-cases/`) state exactly *how*.

---

## SCN-01 — Bulk Module Status Actions Respect Selection State

**Area:** Admin module management
**Objective:** Confirm that bulk publish/unpublish controls behave correctly based on the actual status of the modules selected, rather than only checking whether a selection exists.

**Coverage implied:**

* Single-item selection, all one status
* Multi-item selection, all one status
* Mixed-status selection (some draft, some published)
* Zero-item selection (controls should be inactive)

---

## SCN-02 — Answer Option Validation on Question Creation

**Area:** Admin content authoring
**Objective:** Confirm that answer options entered when creating a question are validated for uniqueness, length, and meaningful content before the question can be saved.

**Coverage implied:**

* Duplicate answer values (exact match, case variation, whitespace variation)
* Empty or whitespace-only answer values
* Answer text at and beyond a defined maximum length
* Valid, fully distinct answer set (control case — should pass without friction)

---

## SCN-03 — Form Data Survives Unintended Navigation

**Area:** Admin content authoring
**Objective:** Confirm that in-progress form data is not silently lost on refresh, back navigation, or accidental tab close, and that the user is warned before losing unsaved work.

**Coverage implied:**

* Refresh mid-entry
* Browser back navigation mid-entry
* Tab close mid-entry
* Confirmed navigation away with no unsaved changes present (should not prompt)
