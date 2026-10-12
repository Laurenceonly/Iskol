---
name: iskol-cross-layer-feature
description: Develop ISKOL features spanning Next.js routes or components and Supabase data access, authorization, or shared contracts. Use for coordinated application changes, not documentation-only edits or standalone visual styling.
---

# ISKOL cross-layer feature development

Read `AGENTS.md` and `knowledge.md` from the repository root. Inspect Git status and distinguish committed code from unrelated pending changes before choosing the affected layers.

## Trace the contract

1. Locate the route, form/display components, Supabase queries or RPC caller, profile/ownership checks, and every consumer of the changed fields. The backend is Supabase; do not invent a separate API service.
2. Before changing Next.js routing, caching, rendering, or configuration, read the relevant installed guide in `node_modules/next/dist/docs/`. Cache Components is enabled. Keep browser state/events in small client boundaries; use the existing server/browser Supabase helper appropriate to the runtime.
3. Record required fields, nullable values, statuses, relationships, and request/result shapes from actual callers. For example, notes use `user_id`, optional `subject_id`, title/content, and active status; schedules use `subject_id`, weekday, times, and optional location.
4. Database definitions are not versioned here. Obtain confirmed schema, RLS, and RPC definitions before changing constraints or database permissions. Document that dependency if it cannot be verified; do not invent migrations against an assumed schema.

## Implement the coordinated change

- Preserve the existing authenticated student/admin boundaries and suspended-account behavior. Route redirects and hidden controls do not replace RLS or RPC authorization. Derive ownership from the session and verify any referenced subject belongs to an authorized workspace.
- Validate inputs at the form and authoritative database/server boundary. Preserve existing nullable/status conventions and ensure old records still render. Coordinate producers and consumers rather than renaming a field in one component only.
- Handle query and mutation failures explicitly, preserve entered data for correction, and confirm success only after the write succeeds. Refresh affected lists without changing unrelated workspace state.
- Use existing Tailwind/shared component patterns and preserve desktop/mobile access. Keep prototype/sample data separate from production Supabase flows.

## Verify and hand off

Run lint and build for affected application code; do not add or run automated tests unless requested. With an authorized development account, check the changed workflow, blank/invalid values, mutation failure, and unauthorized access. Do not perform live destructive actions merely for verification. Report what was checked versus unverified database or browser behavior.

Review the diff for unrelated changes, secrets, compatibility gaps, and all affected consumers. Update `knowledge.md` when facts materially change. Report the behavior, files, checks, and outstanding backend dependencies. Git integration remains subject to user authorization.
