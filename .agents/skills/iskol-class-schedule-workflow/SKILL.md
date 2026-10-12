---
name: iskol-class-schedule-workflow
description: Maintain ISKOL recurring class schedule creation and its subject-detail, dashboard, and calendar consumers. Use when changing weekday/time rules, subject linkage, schedule permissions, or schedule error handling.
---

# ISKOL recurring class schedule workflow

Consult root `AGENTS.md` and `knowledge.md`. Trace `app/subjects/[id]/page.tsx`, `app/calendar/page.tsx`, and `app/dashboard/page.tsx` before editing. These share the `subject_schedules` contract; inspect their current versions because local redesign work may be pending.

## Business rules and data integrity

- A recurring class is linked to an existing subject through `subject_id`. Current writes contain `day_of_week`, `start_time`, `end_time`, and optional `location`.
- Preserve weekday encoding: `0` Sunday, `1` Monday, through `6` Saturday. A Monday-first visual layout does not change the stored encoding.
- Require both times and preserve the current same-day rule: end time must be later than start time. Reject equal/reversed times. Do not introduce overnight classes without an explicit product decision and coordinated consumer changes.
- Trim location and store an empty value as `null`. Preserve sorting by weekday then start time in subject details and by start time in calendar/dashboard queries.
- Supabase can return subject joins as an object or array; preserve the normalization and tolerate absent subjects in display code.

## Authorization and mutation procedure

1. Confirm the route session/proxy guard and subject-loading behavior. A subject ID in a URL is not proof of ownership. Verify database RLS authorizes reading and modifying schedules through the linked subject; definitions are absent locally, so request verified definitions before modifying that contract.
2. Preserve loading/not-found/error states when fetching the subject and schedules. Do not turn a failed schedule query into a misleading empty success state.
3. Validate weekday and time values. Disable duplicate submission while saving. On insertion failure, show the error and retain the form values; on success, close/reset the form and reload that subject's schedules.
4. If schedule fields or timing behavior change, coordinate detail forms, database contracts, calendar recurrence, and dashboard selection in the same feature scope. Keep local date and weekday handling consistent; investigate server/browser timezone differences before claiming parity.

## Verification checklist

Use an authorized development workspace to verify a normal class, Sunday and Monday mapping, an empty location, equal/reversed times, multiple classes ordered correctly, and a failed insert/reload. Check display in subject details, calendar, and dashboard. Verify another account cannot access or mutate the linked subject's schedules only with approved test accounts and database evidence.

Run lint/build for code changes; do not add or run tests unless requested. Report any live checks not performed and any database policy still unverified. Do not alter real users' schedules or deploy schema changes without authorization.
