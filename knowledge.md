# ISKOL project knowledge

## What this project is

ISKOL is a student workspace for organizing subjects, class schedules, tasks, notes, and study planning. The repository implements a **web application** with responsive layouts intended to work in desktop and mobile browsers. It is not currently a native iOS or Android application: there is no Expo/React Native project, native platform folder, or mobile build configuration in the repository.

## Stack

- **Language:** TypeScript for application code, with TSX for React components. CSS is used for styling; configuration also includes JavaScript module files.
- **Framework:** Next.js App Router, with React 19.
- **Runtime/UI:** React Server Components are the default in the App Router; selected interactive screens/components use client-side React.
- **Styling:** Tailwind CSS 3, project CSS in `app/globals.css` and the prototype stylesheet, plus reusable UI components in `components/ui/`.
- **Backend/data/auth:** Supabase JavaScript client and `@supabase/ssr`, using browser and server client helpers in `lib/supabase/`. Auth session cookies are refreshed through `proxy.ts`.
- **Supporting UI packages:** Radix UI primitives, `lucide-react` icons, `next-themes`, and `clsx`/`tailwind-merge` helpers.

## Repository map

- `app/`: App Router pages, layouts, route handlers, and route-specific styles. The committed baseline includes dashboard, subjects, notes, calendar, profile, admin, and auth. Additional local routes are identified below.
- `components/`: Shared application components and small UI primitives.
- `lib/`: Shared helpers and Supabase browser/server setup; local pending work also includes shared legal content.
- `docs/`: Setup evidence and project notes; pending application work includes legal-launch preparation.
- `public/`: Static assets.
- `next.config.ts`: Next.js configuration; Cache Components are enabled.
- `.env.example`: Names of the Supabase public URL and publishable key needed for local configuration. Keep actual credentials private.
- `.agents/skills/`: Repository-specific Codex skills for cross-layer features and the recurring class schedule workflow.

## Important conventions

- Use `app/` routing conventions and check the installed Next.js documentation in `node_modules/next/dist/docs/` before editing Next-specific behavior. The installed Next.js version can differ from familiar examples and may have breaking changes.
- Keep server-only work on the server. Use `lib/supabase/server.ts` from server components and `lib/supabase/client.ts` from client components; do not import server-only modules into client code.
- Pages and components are server-rendered by default. Mark a file with `"use client"` only when it needs client state, effects, browser APIs, or event handlers.
- The `@/*` import alias points to the repository root. TypeScript strict mode is enabled.
- `proxy.ts` refreshes Supabase auth sessions and protects the configured signed-in routes. Maintain its cookie handling when changing auth behavior.
- Make browser layouts responsive, including for phone-sized screens, while remembering that the product is still a web app.

## Local development

1. Install dependencies with `npm install`.
2. Copy `.env.example` into a local environment file and set the Supabase project URL and publishable key.
3. Run `npm run dev` and open the local URL printed by Next.js.

Useful scripts are `npm run build` and `npm run lint`. The README describes current product features and launch status.

## Core workflows and roles

- Entry and authentication: `app/page.tsx` checks the session and profile, sends suspended users to `/auth/suspended`, administrators to `/admin`, and students to `/dashboard`. Auth pages handle signup, email confirmation, sign-in, password recovery, and reset; `app/auth/confirm/route.ts` verifies Supabase OTP links.
- Subjects: students create a subject with name and optional code/instructor, then use `app/subjects/[id]/page.tsx` to add recurring class schedules. Schedules are linked by `subject_id`; weekday values match JavaScript (`0` Sunday through `6` Saturday). End time must be later than start time; blank location becomes `null`.
- Schedule consumers: the dashboard displays today's classes and the calendar reads recurring schedules. Any change to weekday/time semantics affects both consumers. The baseline calendar offers month/week views; pending local work replaces it with a selected-day agenda.
- Notes: students create active notes, optionally link them to a subject, and edit title/content in the note detail route. Creation uses the authenticated `user_id`; an empty subject selection is stored as `null`.
- Profile: students edit optional identity/school/age fields and save `theme_preference`; appearance uses `next-themes`.
- Administration: `app/admin/page.tsx` checks `profiles.is_admin` before calling `get_admin_analytics`, `get_admin_growth`, and `get_admin_users`. `components/admin-user-action.tsx` calls `admin_set_user_status` with `target_user_id` and `new_status` to suspend/reactivate an account.

## API and database boundaries

Application components use Supabase directly rather than a separate custom REST backend. Observed table names are `profiles`, `subjects`, `subject_schedules`, `notes`, and `tasks`; joins associate schedules/notes with subjects. These are code-observed contracts, not a verified database schema. Supabase Auth supplies sessions and email flows. `lib/supabase/server.ts` uses request cookies, `lib/supabase/client.ts` creates the browser client, and `proxy.ts` refreshes sessions on its configured protected routes. `lib/supabase/proxy.ts` is a separate helper; verify callers before changing either file.

Environment configuration uses `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`, as listed in `.env.example`. The repository has no migration directory, schema SQL, RLS policy definitions, RPC implementations, or automated test script. Confirm those remotely with the operator before relying on exact constraints or changing permissions. Never add real environment values to documentation.

## Pending local application work at setup time

The setup branch was created at `b1a2bc1` with unrelated application changes already staged. They are excluded from the Codex setup commit. The local working tree includes a workspace redesign, `/tasks`, `/terms`, `/privacy`, legal dialogs/content, and sample-data routes under `app/prototypes/today/`. Those routes must not be described as shipped by the setup commit. Local pending work also adds the Tasks proxy matcher and device-local accent/custom-color/font persistence under `iskol-appearance`. Check current Git status before relying on those features in a fresh checkout.

## Verification and known limitations

- Installed Next.js at audit time is `16.3.5`; `package.json` declares `next` as `latest`, so consult the installed docs rather than assuming a fixed API version. React is 19 and Tailwind is 3.
- The complete local application working tree passed build and lint before this setup activity; lint retained three warnings (profile/subjects hook dependencies and a prototype image). This does not prove that hosted database policies or email workflows are correct.
- The README's calendar description matches the committed baseline but differs from pending local redesign work. Hosting status, production configuration, data retention, and database policies were not independently verified.
- User-level provider skills are available in this environment but are not installed by cloning this repository. See `docs/codex-setup-report.md` for verified sources and paths.
