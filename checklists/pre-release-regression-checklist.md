# Pre-Release Regression Checklist

A reusable checklist run before any release, covering the areas most likely to regress silently — the kind of thing that passes a quick glance but breaks under actual use. Items are phrased as specific, checkable questions rather than broad statements, since a vague item like "the page works correctly" cannot be verified consistently by different testers.

## Functional

- [ ] Does every primary user flow (login, core task completion, logout) complete without error?
- [ ] Do previously fixed defects remain fixed (spot-check against the last two releases' bug reports)?
- [ ] Do form submissions save the expected data and reject invalid data with a clear message?
- [ ] Does bulk/batch functionality behave correctly across single-item, multi-item, and mixed-state selections?

## UI / Visual

- [ ] Does the layout hold at common breakpoints (mobile, tablet, desktop)?
- [ ] Are loading and empty states visually distinct from populated states (e.g. a 0% chart does not render as if it were 100%)?
- [ ] Is text contrast readable against its background, particularly for secondary/metadata text?
- [ ] Are breadcrumbs, headers, and navigational elements positioned consistently with the rest of the app?

## Data Integrity

- [ ] Does refreshing mid-form lose data silently, or is the user warned first?
- [ ] Do duplicate or near-duplicate entries get caught where uniqueness matters?
- [ ] Does data persist correctly across navigation, not just on the page it was entered on?

## Security (Baseline)

- [ ] Do state-changing requests carry a CSRF token or equivalent protection?
- [ ] Are authentication and session checks enforced on every protected route, not just the entry point?
- [ ] Do response headers include baseline protections (CSP, appropriate cache-control on sensitive pages)?

## Performance

- [ ] Does the primary page load within the agreed target (e.g. under 3s)?
- [ ] Are large images or assets compressed and appropriately sized before deploy?

## Sign-Off

- [ ] All failed items logged as individual bug reports with severity and priority assigned
- [ ] No unresolved Critical or Major findings blocking this release
