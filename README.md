# ClubLend — Robotics Club Equipment Lending

A responsive equipment-library workspace for a university robotics club. The interface uses an editorial workshop direction: graphite surfaces, concrete neutrals, signal-orange accents, Bricolage Grotesque and Hanken Grotesk typography, and subtle motion with reduced-motion support. The homepage now features a custom animated engineering hero rather than the former stock ruler.

## Included

- Next.js 15, React 19 and TypeScript application.
- Responsive navigation, catalogue, requests, loans and returns, members, activity log and settings.
- Role-specific preview access: Admin and Moderator can open Settings; Admin and Secretary can approve/reject requests and process returns.
- Persistent browser-preview settings, including borrowing duration, grace period, pending-request limit and reputation rules. New requests calculate their due date from the configured borrowing period.
- Action-driven activity history and a notification popover with unread/read states and an empty state.
- Reputation starting at 0, on-time return rewards, late-return penalties, non-return penalties, donation awards, Admin adjustments with required reasons, and a transaction ledger recording actor and timestamp. Request priority considers reputation, declared project deadlines and competition urgency, without auto-approval.
- Six AI-generated member portrait assets (male and female) and nine generated equipment catalogue images.
- Supabase client authentication integration and a PostgreSQL schema foundation.

## Run locally

Requirements: Node.js 20.9 or newer.

```bash
npm install
cp .env.example .env.local
npm run dev
```

Open http://localhost:3000.

## Supabase setup

1. Create a Supabase project.
2. Copy the Project URL and publishable/anon key into `.env.local` as `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`.
3. Run `supabase/schema.sql` in the Supabase SQL Editor on a fresh project.
4. Create a user through Supabase Auth. The trigger creates a member profile automatically.
5. Promote the first administrator only after verifying the user's UUID in Authentication → Users.

Never put a Supabase service-role key in a browser environment variable or expose it with a `NEXT_PUBLIC_` prefix.

## Important implementation boundary

This deliverable is a **working front-end preview and integration foundation, not a production-ready multi-user lending system**. The catalogue, requests, member records, preferences, reputation transactions, activity and notifications in these screens are persisted in the current browser's local storage. The role selector is a preview control, not an authorization mechanism. Supabase email/password sign-in is wired when credentials are configured, and the included SQL provides a database/RLS foundation, but the screens are not yet connected to live Supabase CRUD/RPC workflows. Atomic inventory allocation, group borrowing, competition/reputation priority scoring, donation approval workflow, and server-side audit writes still require backend integration and testing.

The reputation donation action in this preview converts an approved BDT donation value into points at 1 point per ৳1,000 (rounded, minimum 1); this is a configurable preview rule, not a verified club policy. The generated member portraits are illustrative sample identities, not real club member photos.
