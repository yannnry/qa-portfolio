# SEC-01 — Missing CSRF Token on Form Submission

**Type:** Security Risk
**Severity:** Major
**Priority:** High
**Reproducibility:** Always

## Location

Admin — Add Question form (state-changing submission request)

## Environment

Production build, tested via browser DevTools network inspection

## Description

The form's submission request carries no CSRF token — none in the request payload, none in a custom header. Without a token to validate, the server has no way to confirm a state-changing request actually originated from the platform's own interface rather than a page hosted elsewhere.

## Steps to Reproduce

1. Open the Add Question form as an authenticated admin.
2. Open DevTools → Network tab.
3. Submit the form and inspect the outgoing request.
4. Check the request body and headers for a CSRF-style token (e.g. `_csrf`, `X-XSRF-TOKEN`).

## Expected Behavior

A unique, per-session CSRF token should be present in every state-changing request and validated server-side before the action is processed.

## Actual Behavior

No token is present in either the payload or the headers. The request would be processed the same way regardless of its origin.

## Impact

An attacker able to get a logged-in admin to visit a malicious page could potentially craft a hidden form there that submits state-changing requests on the admin's behalf, without the admin's knowledge or consent. This finding produces no visible symptom during normal use, which is why it surfaced through network inspection rather than UI testing.

## Recommended Fix

* Enable CSRF middleware server-side to generate and validate a unique token per session.
* Ensure the frontend automatically attaches this token to the headers of every POST, PUT, and DELETE request.

## Status

Open — reported, fix not yet verified.
