# Mergedialix – Project Context

SIM-based mobile CRM for sales teams. Reps use their own Android phone and SIM; calls, leads, tasks and follow-ups sync into one CRM. Managers see team activity on a web dashboard.

Full requirements live in the PRD (keep a copy at `docs/PRD.md`). When a task says "see PRD section X", read that section first.

## Stack (fixed, do not change)

- **API:** Node.js 20, Express, TypeScript, Mongoose
- **Database:** MongoDB Atlas (replica set)
- **Dashboard:** Next.js (App Router), TypeScript, Tailwind CSS
- **Mobile:** Native Android (Kotlin)
- **Validation:** Zod (shared schemas in `packages/`)
- **Auth:** JWT access token (15 min) + rotating refresh token (30 days), bcrypt for passwords
- **Jobs:** BullMQ + Redis
- **Storage (v1.1):** S3-compatible bucket, pre-signed URLs
- **Tests:** Jest, Supertest, mongodb-memory-server (replica set)

## Repo layout

```text
mergedialix/
  api/        Express API
    src/models  routes  controllers  middleware  services  jobs
  web/        Next.js dashboard
  mobile/     Android app
  packages/   shared Zod schemas and types
  docs/       PRD.md
```

## Non-negotiable rules

1. **Tenant isolation.** Every collection except `companies` has `companyId`. All queries go through the tenant plugin, which adds `companyId` to every find, update and delete. A query without tenant context must throw. Never accept `companyId` from the request body or query string; take it from the verified JWT.
2. **Role scope.** Rep: only own records (`ownerId`, `repId`, `assignedTo`). Manager: own team. Admin: whole company.
3. **Validate all input** with Zod at the route boundary. Reject unknown fields.
4. **Phone numbers** are stored in E.164 format. Normalise before saving or matching.
5. **Call sync is idempotent.** Upsert on `{ repId, deviceCallId }`.
6. **Secrets** only in `.env`. Never log tokens, passwords, OTPs or full phone numbers.
7. **Every route needs a cross-tenant test**: a user from company A must get 404 or 403 for company B data.
8. **Errors** return `{ code, message, details }` with the correct HTTP status. No stack traces in responses.
9. **No direct database access** from the dashboard or the mobile app. Everything goes through the API under `/api/v1`.

## Coding conventions

- TypeScript strict mode. No `any` without a comment explaining why.
- Controllers stay thin; business logic lives in `services/`.
- Async route handlers use a shared error-catching wrapper.
- Use cursor pagination for list endpoints.
- Name files in kebab-case, types in PascalCase, env vars in UPPER_SNAKE_CASE.
- Small commits, one slice per branch.

## How to work on a task

1. Read the PRD section named in the task and this file.
2. Reply with a short plan (files to create or change) before writing code.
3. Implement only what the task asks. Do not add extra features.
4. Write tests with the code, then run them and show the result.
5. List anything you assumed or left out.

## Build order

1. API setup, MongoDB connection, models and indexes
2. Auth (OTP, login, refresh, logout) and tenant middleware
3. Leads, notes and tasks APIs
4. `POST /calls/sync` and call listing
5. Next.js dashboard: login, leads, team overview
6. Android app: login and leads first, then call log sync
7. v1.1: recording upload, auto dialler, GPS
8. v1.2: WhatsApp, email, external CRM integrations

## Known risks to remember

- Android restricts third-party call recording on newer versions. Check official Android docs and test on real devices before writing recording code.
- Google Play restricts Call Log permissions. Use APK distribution for pilots.
- Recording and GPS need explicit employee consent and clear in-app disclosure.
