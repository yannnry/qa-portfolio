# Test Cases — Answer Option Validation (derived from SCN-02)

Applying equivalence partitioning to the answer-option field: values are grouped into partitions expected to be handled the same way, then one representative case is tested per partition, with duplicate-detection treated as its own partition since it depends on comparing multiple values rather than validating one in isolation.

| Partition | Represents |
|---|---|
| P1 — Valid, fully distinct | Normal expected input |
| P2 — Exact duplicate | Same string entered twice |
| P3 — Case-variant duplicate | Same string, different casing |
| P4 — Whitespace-variant duplicate | Same string, leading/trailing spaces |
| P5 — Empty / whitespace-only | No meaningful content |
| P6 — At maximum length | Boundary value |
| P7 — Beyond maximum length | Just past the boundary |

---

**TC-01 — Valid, fully distinct answer options (P1)**

| Field | Value |
|---|---|
| Preconditions | Admin is on the Add Question form |
| Steps | 1. Enter question text.  2. Enter four distinct, non-empty answer options.  3. Submit. |
| Expected Result | Question saves successfully with no validation errors. |

**TC-02 — Exact duplicate answer options (P2)**

| Field | Value |
|---|---|
| Preconditions | Admin is on the Add Question form |
| Steps | 1. Enter question text.  2. Enter "Yes" as two separate answer options.  3. Submit. |
| Expected Result | Submission is blocked with a validation message identifying the duplicate. |

**TC-03 — Case-variant duplicate ("Yes" vs. "yes") (P3)**

| Field | Value |
|---|---|
| Preconditions | Admin is on the Add Question form |
| Steps | 1. Enter question text.  2. Enter "Yes" and "yes" as two answer options.  3. Submit. |
| Expected Result | Treated as a duplicate; submission blocked with the same validation message as TC-02. |

**TC-04 — Whitespace-variant duplicate ("Yes" vs. " Yes ") (P4)**

| Field | Value |
|---|---|
| Preconditions | Admin is on the Add Question form |
| Steps | 1. Enter question text.  2. Enter "Yes" and " Yes " (with leading/trailing spaces) as two answer options.  3. Submit. |
| Expected Result | Values are trimmed before comparison; treated as a duplicate, submission blocked. |

**TC-05 — Whitespace-only answer option (P5)**

| Field | Value |
|---|---|
| Preconditions | Admin is on the Add Question form |
| Steps | 1. Enter question text.  2. Enter a string of only spaces as one answer option.  3. Submit. |
| Expected Result | Blocked with a validation error attributed to that specific answer field. |

**TC-06 — Answer text at maximum length (P6)**

| Field | Value |
|---|---|
| Preconditions | Admin is on the Add Question form; max length is defined (e.g. 200 characters) |
| Steps | 1. Enter question text.  2. Enter an answer option of exactly the maximum allowed length.  3. Submit. |
| Expected Result | Accepted without error. |

**TC-07 — Answer text beyond maximum length (P7)**

| Field | Value |
|---|---|
| Preconditions | Admin is on the Add Question form; max length is defined (e.g. 200 characters) |
| Steps | 1. Enter question text.  2. Enter an answer option one character past the maximum length.  3. Submit. |
| Expected Result | Blocked, or input is prevented from exceeding the limit at the field level. |

---

**Traceability:** TC-01 through TC-07 → SCN-02. TC-02 through TC-04 correspond to the duplicate-detection defect class documented in `bug-reports/` (see BUG-01 in `case-studies/02-add-question-testing.md`) — these cases show what should have caught it.
