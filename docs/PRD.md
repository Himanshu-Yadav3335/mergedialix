# Mergedialix – SIM-Based Mobile CRM

**Product Requirements Document (PRD)** · Version 1.0 (Final) · November 15, 2026

*Source: derived from a 51-second promo video (on-screen text and visuals only). The tech stack is fixed (Next.js, Node.js with Express, MongoDB). Pricing and platform details were not shown in the video, so those parts are proposals to be validated.*

## 1. Overview

Mergedialix is a **SIM-based mobile CRM** for sales teams. Instead of cloud telephony, it uses the employee's own phone and SIM to place calls, then logs, records and organises every interaction into one centralised CRM. The promise: *Track Calls. Manage Leads. Drive Sales.*

**One-line pitch:** Your mobile + your SIM = one centralised CRM, with no separate dialler, no expensive telephony setup and no separate CRM.

## 2. Problem Statement

Small and mid-sized sales teams (telecallers, field sales, inside sales) make most of their calls from personal or company mobiles. Managers cannot see:

- how many calls each rep made, to whom, and for how long;
- what happened on each lead and what the next step is;
- whether follow-ups are being missed.

Cloud telephony and enterprise CRMs solve this but are expensive, need setup (virtual numbers, hardware, integrations) and change how reps call. Teams need a lightweight option that works with the phone and SIM they already use.

## 3. Goals and Non-Goals

### Goals

1. Automatically capture every call made or received on a rep's SIM and attach it to the right lead.
2. Give reps one app for leads, tasks and follow-ups, so nothing is missed.
3. Give managers real-time visibility into team activity and performance.
4. Be live in under 15 minutes per team: install, log in, start calling.
5. Connect to existing CRMs so data is not locked in.

### Non-Goals (v1)

- Cloud telephony, virtual numbers or IVR.
- iOS app (iOS does not allow call log or call recording access for third-party apps).
- Built-in WhatsApp Business API messaging campaigns.
- AI call scoring or transcription (candidate for v2).

## 4. Target Users

| Persona | Description | Key needs |
| --- | --- | --- |
| **Sales Rep / Telecaller** | Makes 30–150 calls a day from an Android phone | Fast dialling, auto-logged calls, clear daily task list, no manual data entry |
| **Team Lead / Sales Manager** | Manages 5–50 reps | Live activity view, call recordings, follow-up compliance, reports |
| **Business Owner / Admin** | Owns the account | Add or remove users, set permissions, integrations, billing, data control |

**Ideal customer:** SMBs in real estate, education/admissions, insurance, finance, solar and local services, where sales run over phone and WhatsApp.

## 5. Product Scope

### 5.1 MVP (v1.0)

- User, team and role management
- Lead management (create, import, assign, status)
- Tasks and follow-ups with calendar
- Click-to-call from the app
- Automatic call log sync (incoming, outgoing, missed, duration)
- Manager dashboard with basic reports

### 5.2 v1.1

- Call recording and playback
- Auto dialler
- Live GPS location (opt-in, shift hours only)

### 5.3 v1.2+

- WhatsApp call logs (audio and video) and WhatsApp Web integration
- Email integration
- External CRM integration (webhooks and REST API, then native connectors)
- Advanced analytics, AI call summaries

## 6. Functional Requirements

Priority: **P0** = must have for the release, **P1** = should have, **P2** = nice to have.

### 6.1 Authentication and Accounts

| ID | Requirement | Priority |
| --- | --- | --- |
| AUTH-1 | Login with phone number and OTP, or email and password | P0 |
| AUTH-2 | Roles: Admin, Manager, Rep, each with distinct permissions | P0 |
| AUTH-3 | Admin can invite, deactivate and reassign users | P0 |
| AUTH-4 | Deactivating a user instantly revokes app access | P0 |

### 6.2 Lead Management

| ID | Requirement | Priority |
| --- | --- | --- |
| LEAD-1 | Create leads manually or import from CSV or Excel | P0 |
| LEAD-2 | Lead fields: name, phone(s), email, source, status, owner, tags, notes | P0 |
| LEAD-3 | Assign leads to reps manually or by round-robin | P0 |
| LEAD-4 | Lead timeline showing calls, notes, tasks and status changes | P0 |
| LEAD-5 | Duplicate detection by phone number | P1 |
| LEAD-6 | Custom statuses and pipeline stages | P1 |

### 6.3 Tasks and Follow-Ups

| ID | Requirement | Priority |
| --- | --- | --- |
| TASK-1 | Create a task or follow-up on a lead with date, time and note | P0 |
| TASK-2 | Calendar and list view of today's, upcoming and overdue follow-ups | P0 |
| TASK-3 | Push reminders before a follow-up is due | P0 |
| TASK-4 | Prompt the rep to log outcome and next follow-up after each call | P1 |

### 6.4 Calling and Call Tracking

| ID | Requirement | Priority |
| --- | --- | --- |
| CALL-1 | Click-to-call opens the phone dialler with the lead's number, using the rep's SIM | P0 |
| CALL-2 | Automatically log incoming, outgoing and missed calls with number, time and duration | P0 |
| CALL-3 | Match logged calls to existing leads by phone number; unknown numbers can be saved as new leads | P0 |
| CALL-4 | Post-call screen to set disposition (connected, not reachable, interested, etc.), note and follow-up | P1 |
| CALL-5 | Dual-SIM support: record which SIM was used | P1 |
| CALL-6 | Only business calls are synced; personal numbers can be excluded | P0 |

### 6.5 Call Recording (v1.1)

| ID | Requirement | Priority |
| --- | --- | --- |
| REC-1 | Record calls on supported devices and upload to secure storage when on Wi-Fi or mobile data | P0 |
| REC-2 | Play back recordings from the lead timeline and manager dashboard | P0 |
| REC-3 | Admin-configurable retention period and auto-delete | P1 |
| REC-4 | Consent notice and a per-company recording toggle | P0 |

### 6.6 Auto Dialler (v1.1)

| ID | Requirement | Priority |
| --- | --- | --- |
| DIAL-1 | Rep selects a list of leads and the app dials them one after another | P0 |
| DIAL-2 | Automatic next-lead prompt after call ends and disposition is saved | P0 |
| DIAL-3 | Configurable delay between calls, and skip or pause controls | P1 |

### 6.7 Live GPS Location (v1.1)

| ID | Requirement | Priority |
| --- | --- | --- |
| GPS-1 | Opt-in location tracking only during configured working hours | P0 |
| GPS-2 | Manager can view rep locations on a map and location at the time of calls or visits | P1 |
| GPS-3 | Clear in-app indicator when tracking is active | P0 |

### 6.8 WhatsApp and Email (v1.2)

| ID | Requirement | Priority |
| --- | --- | --- |
| WA-1 | Log WhatsApp audio and video call history against leads | P1 |
| WA-2 | Open a WhatsApp chat with a lead from the app with message templates; WhatsApp Web integration for desktop | P1 |
| MAIL-1 | Connect an email account to send and log emails on the lead timeline | P2 |

### 6.9 External CRM Integration (v1.2)

| ID | Requirement | Priority |
| --- | --- | --- |
| INT-1 | Public REST API and webhooks for leads, calls and tasks | P0 |
| INT-2 | Two-way sync with popular CRMs via connectors (for example Zoho, HubSpot, Salesforce), prioritised by customer demand | P1 |
| INT-3 | API keys and access logs managed by Admin | P0 |

### 6.10 Manager Dashboard and Reports

| ID | Requirement | Priority |
| --- | --- | --- |
| DASH-1 | Team view: calls made, connected calls, talk time, missed calls and follow-ups due, per rep and per day | P0 |
| DASH-2 | Lead funnel by status and source | P1 |
| DASH-3 | Filter by date range, team and rep; export to CSV | P1 |
| DASH-4 | Alerts for inactivity and overdue follow-ups | P2 |

## 7. Non-Functional Requirements

- **Platform:** Android 10+ for the rep app; responsive web dashboard (Chrome, Edge, Safari).
- **Performance:** app cold start under 3 seconds; call log appears in the dashboard within 30 seconds of the call ending on a normal connection.
- **Offline:** the app works offline and queues call logs, notes and recordings, syncing when the network returns.
- **Battery and data:** background sync must stay lightweight (target under 3% battery per day from the app).
- **Security:** encryption in transit and at rest, tenant isolation enforced in the API on every query, role-based access, audit logs.
- **Privacy and compliance:** explicit employee consent, in-app disclosure of what is tracked, call recording consent per local law, data deletion on request, alignment with India's DPDP Act and other regional rules as applicable.
- **Reliability:** 99.5% uptime target for backend services.
- **Scale (initial):** up to 500 companies, 10,000 reps, 1 million calls per month.

## 8. Technical Architecture

The stack is fixed: Next.js for the dashboard, Node.js with Express for the API, MongoDB for data. The Android app and the dashboard use the same REST API.

### 8.1 Stack

| Layer | Choice | Notes |
| --- | --- | --- |
| Web dashboard | Next.js (App Router), TypeScript, Tailwind CSS | Server components for reports; client components for tables and forms |
| API | Node.js 20 LTS, Express, TypeScript | Stateless REST API, versioned under /api/v1 |
| Database | MongoDB Atlas (replica set) with Mongoose | Transactions need a replica set; Atlas M10 or higher for production |
| Auth | JWT access token (15 min) + rotating refresh token (30 days) | Passwords hashed with bcrypt; OTP through an SMS provider |
| Validation | Zod | Schemas shared by API and dashboard |
| File storage | S3-compatible bucket (AWS S3 or Cloudflare R2) | Recordings use pre-signed URLs and are never stored in MongoDB |
| Push notifications | Firebase Cloud Messaging | Follow-up reminders and assignment alerts |
| Background jobs | BullMQ with Redis | Reminders, CSV import, report export, retention cleanup |
| Mobile app | Native Android (Kotlin) | Call log, foreground service and recording need native APIs |
| Hosting | API on Render, Railway or AWS; dashboard on Vercel | Region chosen for customer data residency |
| Observability | Pino logs, Sentry, uptime checks | Request ID on every log line |

### 8.2 Architecture

All clients go through one Express API. MongoDB is reached only from the API, never from a client.

- **Android app:** reads the call log, syncs calls in batches, shows leads and tasks, uploads recordings straight to object storage with a pre-signed URL.
- **Next.js dashboard:** manager and admin screens; calls the API with the user's JWT and has no direct database access.
- **Express API:** auth, tenant scoping, business rules, webhooks, rate limiting.
- **MongoDB:** system of record. **Object storage:** recordings. **Redis with BullMQ:** reminders and imports. **FCM:** push notifications.

&#91;embedded content: architecture · 2 clients, 1 API, 4 services\]

The Express API is the only door to MongoDB, storage, queues and notifications.

### 8.3 Repository layout

```text
mergedialix/
  api/        Express + TypeScript
    src/models  routes  controllers  middleware  services  jobs
  web/        Next.js dashboard
  mobile/     Android app
  packages/   shared Zod schemas and types
```

### 8.4 Data model (MongoDB collections)

Every document except `companies` carries `companyId`. Phone numbers are stored in E.164 format so calls match leads reliably.

| Collection | Key fields | Indexes |
| --- | --- | --- |
| companies | name, plan, settings (recordingEnabled, retentionDays) | none beyond \_id |
| users | companyId, name, phone, email, passwordHash, role (admin, manager, rep), managerId, isActive | unique {companyId, phone}; unique sparse {email} |
| leadStatuses | companyId, name, position | unique {companyId, name} |
| leads | companyId, ownerId, statusId, name, phone, altPhone, email, source, tags\[\], createdBy, timestamps | unique {companyId, phone}; {companyId, ownerId, updatedAt} |
| calls | companyId, repId, leadId (optional), phone, direction, startedAt, durationSeconds, simSlot, disposition, note, recording {key, sizeBytes}, deviceCallId | unique {repId, deviceCallId}; {companyId, repId, startedAt desc}; {leadId, startedAt desc} |
| tasks | companyId, leadId, assignedTo, title, note, dueAt, status, completedAt | {assignedTo, status, dueAt} |
| leadNotes | companyId, leadId, authorId, body, createdAt | {leadId, createdAt} |
| refreshTokens | userId, tokenHash, deviceId, expiresAt | TTL on expiresAt |
| auditLogs | companyId, actorId, action, entity, entityId, createdAt | {companyId, createdAt desc} |
| locations (v1.1) | companyId, repId, point (GeoJSON), recordedAt | 2dsphere; TTL by retention |
| apiKeys (v1.2) | companyId, name, keyHash, lastUsedAt | unique {keyHash} |

### 8.5 Multi-tenancy and security

MongoDB has no row-level security, so the API enforces tenant isolation itself:

1. Auth middleware verifies the JWT and puts `userId`, `companyId` and `role` on the request.
2. A Mongoose tenant plugin adds `companyId` to every find, update and delete and sets it on create. A query without tenant context throws an error.
3. Role scope: reps only see records where `ownerId`, `repId` or `assignedTo` is their own id; managers see their team; admins see the whole company.
4. Request bodies are validated with Zod, and `companyId` is never accepted from the client.
5. Login and OTP endpoints are rate limited; Helmet, a CORS allow-list and HTTPS only.
6. Recordings are private objects. Playback uses short-lived signed URLs after a role check.
7. Automated tests check that a user from company A can never read or write company B data on any route.

### 8.6 REST API (v1)

JSON over HTTPS under `/api/v1`. Lists use cursor pagination. Errors return `{ code, message, details }`. Every route needs a valid JWT except the auth routes.

| Area | Endpoints | Access |
| --- | --- | --- |
| Auth | POST /auth/otp/request, /auth/otp/verify, /auth/login, /auth/refresh, /auth/logout | Public, then everyone |
| Users | GET /users, POST /users, PATCH /users/:id, POST /users/:id/deactivate | Admin; list also for manager |
| Leads | GET /leads, POST /leads, GET, PATCH, DELETE /leads/:id, POST /leads/:id/assign, POST /leads/import (CSV) | Rep (own), manager, admin |
| Notes | GET, POST /leads/:id/notes | Rep (own leads), manager, admin |
| Tasks | GET /tasks (due=today, overdue, upcoming), POST /tasks, PATCH /tasks/:id, POST /tasks/:id/complete | Rep (own), manager, admin |
| Calls | POST /calls/sync (batch), GET /calls, PATCH /calls/:id (disposition, note) | Rep (own), manager, admin |
| Recordings (v1.1) | POST /calls/:id/recording/upload-url, POST /calls/:id/recording/confirm, GET /calls/:id/recording/url | Rep (upload), manager, admin |
| Reports | GET /reports/team-activity, /reports/funnel, /reports/export | Manager, admin |
| Integrations (v1.2) | Webhooks and API keys CRUD; public API under /api/v1/public | Admin |

### 8.7 Call sync flow

1. The Android foreground service reads call log entries newer than the last synced timestamp.
2. It normalises numbers to E.164 and builds a batch of up to 100 calls, each with its `deviceCallId`.
3. It sends `POST /calls/sync`. The API upserts on `{repId, deviceCallId}`, so retries never create duplicates.
4. The API matches each number to a lead in the same company. Unmatched calls are kept without a lead and can be turned into one.
5. The API returns a result per call. The app marks them synced and retries failures with exponential backoff.
6. The dashboard refreshes every 15 to 30 seconds in v1; server-sent events can replace polling later.

### 8.8 Recording upload flow (v1.1)

1. The app asks for a pre-signed upload URL for the call.
2. The app uploads the audio file directly to the bucket, on Wi-Fi by default, and retries if it fails.
3. The app calls the confirm endpoint, and the API saves the object key and size on the call.
4. A nightly BullMQ job deletes recordings older than the company's retention period.

### 8.9 Environments and quality

- **Environments:** development, staging and production, each with its own MongoDB cluster and bucket.
- **CI:** GitHub Actions runs lint, type checks and tests on every pull request.
- **Tests:** Jest and Supertest against an in-memory MongoDB replica set, with cross-tenant access tests on every route.
- **API docs:** OpenAPI spec generated from the Zod schemas.
- **Backups:** daily MongoDB snapshots with point-in-time restore; recording bucket versioning on.
- **Secrets:** kept in the host's secret manager, never in the repository.

## 9. Platform Constraints and Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Android restricts third-party call recording on newer versions and some devices | Recording may fail on part of the device base | Maintain a supported-device list; test on top OEMs; consider approved dialler approach; set expectations in sales material |
| Google Play restricts Call Log and SMS permissions and accessibility use | App may be rejected or limited on Play Store | Apply under the permitted default-dialler or core-feature exceptions; use direct APK distribution for pilots |
| OEM battery optimisation kills background sync | Missing call logs | Guided battery-setting onboarding; foreground service; periodic re-sync |
| Employee privacy concerns about GPS and recording | Low adoption, legal exposure | Opt-in, working-hours-only tracking, clear consent, admin transparency |
| WhatsApp call log access is unofficial and may break | Unreliable feature | Ship last, label as best effort |
| Competing established mobile CRMs | Hard differentiation | Focus on fast onboarding, SIM-based simplicity and low price |
| A missing companyId filter in MongoDB leaks one company's data to another | Severe privacy breach and loss of customer trust | Mongoose tenant plugin that throws without tenant context; cross-tenant tests on every route; no direct database access from clients |

## 10. Success Metrics

| Metric | Target (first 6 months) |
| --- | --- |
| Activated teams (at least 5 reps making calls in week 1) | 50 |
| Call capture rate (calls logged vs. actual calls) | 95% or higher |
| Weekly active reps / total invited reps | 70% |
| Follow-up completion rate | 80% |
| Free-demo to paid conversion | 20% |
| Time to onboard a team | Under 15 minutes |

## 11. Release Plan

| Phase | Duration (est.) | Deliverables |
| --- | --- | --- |
| 0. Discovery | 2 weeks | Interviews with 5–10 sales teams, Android permission feasibility spike, final scope |
| 1. MVP build | 8–10 weeks | Auth, leads, tasks, click-to-call, call log sync, basic dashboard |
| 2. Pilot | 4 weeks | 3–5 pilot teams via APK, feedback, stability fixes |
| 3. v1.1 | 6–8 weeks | Call recording, auto dialler, GPS |
| 4. v1.2 | 8–10 weeks | WhatsApp, email, external CRM integrations, advanced reports |

## 12. Open Questions

1. Which Android versions and device brands must be supported for recording at launch?
2. Will distribution be Play Store, direct APK, or both?
3. What is the pricing model (per user per month, tiers, free trial)?
4. Which external CRMs are the highest priority for integration?
5. Which countries and languages does v1 launch in, and what are the local recording laws?
6. Is a web-only manager view enough for v1, or is a manager mobile app needed?
7. How long should recordings and call logs be retained by default?

## 13. Appendix: Features Shown in the Promo Video

SIM-based mobile CRM · Not cloud telephony · Call tracking and recording · Live GPS location · WhatsApp call logs (audio and video) · Auto dialler to speed up outgoing calls · Leads, tasks and follow-ups · WhatsApp Web and email integration · External CRM integration · No separate dialler, no expensive telephony setup, no separate CRM · One mobile-based solution · Call to action: book a free demo.
