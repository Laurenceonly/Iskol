# ISKOL

ISKOL is a web workspace for students who want their class timetable, schoolwork, and notes in one place. Use the dashboard to see which classes meet today and what work is still pending.

## Student workspace

- **Subjects and schedules** — Save a subject’s course code and instructor, then add recurring class times and optional room details.
- **Calendar** — See when classes meet based on the schedules saved under your subjects.
- **Notes** — Keep a standalone note or link it to a subject so it’s easier to find when you study.

## Run locally

ISKOL uses Next.js, TypeScript, Tailwind CSS, and Supabase for authentication and data storage. Sign-in and student workflows require a Supabase project with the ISKOL database schema and access policies in place. Database setup is managed separately.

1. Install dependencies with `npm ci`.
2. Copy [`.env.example`](.env.example) to `.env.local` and fill in your project settings there. The example contains placeholders only.
3. Run `npm run dev` and open `http://localhost:3000`.
