<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

# Project guidance

- Consult `knowledge.md` before planning a feature or changing authentication, data access, or architecture. Distinguish committed functionality from pending local work documented there.
- ISKOL is a responsive web application built with Next.js. Do not treat it as a native iOS/Android app or introduce a mobile app framework unless the product direction changes.
- Before changing Next.js APIs, routing, caching, rendering, or configuration, read the relevant guide under `node_modules/next/dist/docs/`. This project has `cacheComponents: true` in `next.config.ts`; check the matching Cache Components guidance for related changes.
- Use the App Router. Routes, layouts, and route handlers live under `app/`. Components are React with TypeScript (`.tsx`); keep TypeScript strict and use the `@/*` alias for project-root imports.
- App Router components are Server Components by default. Add `"use client"` only when a component needs browser APIs, React state/effects, or event handlers. Keep client boundaries as small as practical.
- Supabase access is split by runtime: use `lib/supabase/server.ts` for server-rendered code and `lib/supabase/client.ts` for browser components. Use the existing `proxy.ts` session refresh/auth pattern. Never expose a service-role secret in client code or commit real environment secrets; use `.env.example` as the template.
- Follow the existing Tailwind CSS and shared UI component patterns (`components/ui/`). Use `lucide-react` for icons where appropriate.
- Prefer focused changes that preserve the current student workspace behavior (subjects, tasks, notes, schedules, profile, and admin flows). Update `knowledge.md` when architectural or product facts materially change.
- Available project commands: `npm run dev`, `npm run build`, and `npm run lint`. Do not add tests or run them unless requested.

# Data, authorization, and verification

- Preserve student and administrator boundaries. Read the relevant route guards and RPC callers before changing permissions; hidden navigation is not authorization. Use the authenticated user's ID for ownership rather than accepting an arbitrary owner from a form.
- Queries using the public Supabase key rely on database authorization. Schema, RLS policies, triggers, and RPC definitions are not versioned here; obtain verified definitions before changing database contracts. Do not claim client validation or proxy redirects enforce database permissions.
- Validate form inputs, preserve existing null/status conventions, handle Supabase errors, and show success only after a successful mutation. Preserve the existing weekday encoding and schedule time rules.
- For application changes, run `npm run lint` and `npm run build` as appropriate and report errors, warnings, and any live workflows not exercised. Documentation-only work requires checking references and consistency; no application tests are required.
- Inspect Git status before editing. Preserve unrelated staged and unstaged work. Commit, push, create a PR, or merge only when authorized; use explicit paths when preparing a scoped commit.

# Project skills

- For a feature spanning routes/components and Supabase data or authorization, use `.agents/skills/iskol-cross-layer-feature/SKILL.md`.
- For recurring class schedule creation or its dashboard/calendar consumers, use `.agents/skills/iskol-class-schedule-workflow/SKILL.md`.
- Provider skills may be installed in user-level locations. Their instructions remain subordinate to the user's requested scope and these repository rules; do not install duplicates merely to make them repository-local.
