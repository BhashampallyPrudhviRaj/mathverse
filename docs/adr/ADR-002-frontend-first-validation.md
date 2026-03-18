# ADR-002: Frontend Validates Before Backend on Obvious Errors

## Status
Accepted

## Date
18-Mar-2026

## Context
During the division-by-zero sequence diagram review, a decision 
was needed: should validation for obvious errors (like B=0 
on division) happen on the frontend, backend, or both?

## Decision
Frontend catches obvious invalid states (empty inputs, B=0 on
divide) BEFORE making any API call. Backend ALWAYS re-validates
independently regardless of frontend behavior.

## Rationale
1. PERFORMANCE: Eliminates unnecessary network round trips for 
trivially detectable errors
2. UX: User gets instant feedback without waiting for API response
3. DEFENSE IN DEPTH: Backend never trusts client input - it
validates independently, protecting against direct API calls
(Postman, curl, other clients bypassing the frontend)

## Consequences
- Frontend and backend both maintain validation logic (small duplication)
- Validation rules must stay in sync between FE and BE
- Backend errors (HTTP 400) still handled gracefully on FE as
a safety net