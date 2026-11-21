# API and data plan

## Architecture and trust boundaries

The current public site is a Vinext/Cloudflare Worker application using D1 and Resend. The reusable dating source is Python FastAPI using Mongo-compatible primitives and a PostgreSQL document adapter. These are different runtimes and data models. Preserve the current Cloudflare deployment; decide whether to host a narrow Python service or deliberately port its domain operations. Record that choice with test parity and a rollback plan. Do not assume D1 can execute the Python service or that old database migrations can be replayed over the live waitlist.

The native client uses a reviewed member API with server-verified member identity. Proposed client stack is Expo/React Native; tokens belong in platform secure storage and are cleared on sign-out/account change. Every object operation derives the member/environment server-side. Client-supplied roles, user IDs, email headers, environment selectors, and successful checkout screenshots cannot authorize reads or writes.

Owner routes require a separate owner boundary. Keep Cloudflare Access passkey sign-in for the exact `osama@imladri.com` identity; preserve the pinned issuer/audience and signature/time validation. No IP restriction and no Gmail owner identity. If FastAPI receives owner requests through a gateway, verify a trusted signed identity proof at the boundary; do not trust a forwarded email header or old `staff` role alone. The mobile app must never possess the owner session or admin secrets.

## Existing dating endpoints

These are **existing source contracts**, formed from `/api` in `backend/server.py` plus `/dating` in `backend/dating/router.py`. They are not asserted to be hosted at `imladri.com` today.

| Existing route | Purpose / input |
| --- | --- |
| `GET /api/dating/bootstrap` | Member/profile/preferences/catalog/launch/membership snapshot; contains historical beta metadata to replace |
| `POST /api/dating/enrollment` | `{version:"dating-enrollment-v1",accepted:true,adult_confirmed:true}` |
| `DELETE /api/dating/enrollment` | `{confirmed:true}`; remove dating participation while retaining unrelated spaces |
| `GET`, `PUT/PATCH /api/dating/profile` | Owner draft; bounded `Profile` input and `expected_revision` |
| `POST /api/dating/profile/submit`, `/profile/state` | Submit review; choose active/paused/draft subject to service rules |
| `GET/POST /api/dating/photos`, `GET /photos/{id}/content`, `DELETE /photos/{id}` | Private photo listing/upload/read/remove; current maximum upload 2 MiB and reviewed publication |
| `GET/PUT /api/dating/preferences` | Reciprocal criteria, optional matching scopes, bounded catalog answers and revision |
| `GET /api/dating/discovery?limit=24` | Current ranked eligible set, not a weekly assignment; limit up to 50 and bounded candidate scan |
| `GET /api/dating/profiles/{id}`, `POST /interests` | Safe profile; `{profile_id,choice:"like"|"pass"}`; must gain batch authorization |
| `GET /api/dating/likes`, `/matches` | Incoming interests/mutual connections; do not copy a separate Likes tab or vanity count automatically |
| `GET/POST /api/dating/matches/{id}/messages`, `POST .../read`, `POST .../unmatch` | Cursor pages; message `{text,request_id}`; participant-only reads/writes |
| `GET/POST /api/dating/blocks`, `DELETE /blocks/{profile_id}` | Member-controlled contact/access restriction |
| `POST /api/dating/reports`, `/appeals` | Bounded incident/category/evidence references and review request |
| `GET/POST/DELETE /api/dating/matches/{id}/sharing` | Selected answers for one match; revision-aware grant and revocation |
| `POST /api/dating/matches/{id}/feedback`, `GET /export` | Own feedback and owner export; not a public score |
| `GET /api/dating/admin/queue`, `/admin/metrics` | Legacy injected admin dependency; replace/bridge owner boundary before reuse |
| `PUT /api/dating/admin/settings` | Legacy single-city profile/discovery switches; not a public waitlist cap |
| `POST /api/dating/admin/profiles/{id}/review`, `/photos/{id}/review`, `/reports/{id}/review`, `/appeals/{id}/review` | Profile review enforces `expected_revision`; photo and report/appeal review currently need equivalent optimistic-concurrency guards added |

`Profile` includes display name, date of birth, gender, city, bio, intent, relationship structure and optional expected revision. `Preferences` includes adult age range, allowed genders/cities/intents/structures, personality/intimacy answers, matching-use toggles and expected revision. Use the schema's enums explicitly. Profile answers are not a validated psychological diagnosis.

**Required authorization adaptation:** the existing member-authenticated `GET /api/dating/photos/{id}/content` route independently permits legacy `admin`, `staff` and `super_admin` roles before the normal photo-access decision. Replacing the `/admin` dependency alone does not remove this shortcut. Replace it with the new verified owner boundary or a narrowly authorized member read; an unrelated member with a legacy role must not gain photo access. Audit all member-route role overrides when extracting the host.

## Proposed mobile API additions

Freeze and publish an OpenAPI contract under `/api/v1` or an equally explicit versioned namespace before generating the native client. The names below are **proposed**, not endpoints the agent may assume already exist.

| Proposed route | Required server behavior |
| --- | --- |
| `GET /api/v1/me` | Current verified member, enrollment/service availability and server entitlements |
| `GET /api/v1/introductions/current` | Persisted batch ID, release/expiry, assigned safe profiles, supported reason facts, each action state |
| `POST /api/v1/introductions/{id}/response` | Accept/pass with stable request ID and expected version; validate assignment, eligibility and expiry atomically |
| `GET/POST /api/v1/connections/{id}/date-plans` | Participant-only plan proposals; create/reschedule idempotently |
| `POST /api/v1/date-plans/{id}/response` | Accept/decline/cancel the specific proposal version; cannot accept for the other person |
| `POST /api/v1/connections/{id}/outcomes` | Optional self-report; explicit unknown/not-yet states and no public disclosure |
| `POST /api/v1/me/devices`, `DELETE .../{id}` | Platform token registration/revocation bound to the authenticated member |
| `GET /api/v1/me/membership`, `POST .../purchases/reconcile` | Server-verified purchase/restore, account ownership and idempotent transaction reconciliation |
| Provider notification endpoint | Verify signed subscription lifecycle events, deduplicate and order by authoritative transaction state |
| `POST /api/v1/me/contact` | Authenticated member contact written into the owner's categorized inbox through a reviewed server adapter |
| `GET /api/v1/me/export`, `POST /api/v1/me/deletion` | Account/data lifecycle, explicit confirmation and accurate subscription guidance |

Keep reusable profile, preferences, connection/chat, block/report and sharing contracts behind the versioned adapter where practical. Provide typed, stable errors for unauthenticated, unauthorized/unavailable, validation, conflict/revision, rate-limit, and retryable server failures. A generic unavailable response should not disclose another user's existence or suspension details.

## Data ownership and persistence

Existing collections are `dating_enrollments`, `dating_profiles`, `dating_preferences`, `dating_photos`, `dating_interests`, `dating_matches`, `dating_messages`, `dating_blocks`, `dating_shares`, `dating_feedback`, `dating_reports`, `dating_appeals`, `dating_events`, `dating_rate`, `dating_settings`, and `dating_moderation`. The service defines indexes and environment scoping. Preserve unique owner/pair/request invariants in any SQL port. Test adapter behavior and index/TTL semantics rather than assuming Mongo-compatible syntax guarantees equivalent isolation.

Add explicit stores for introduction batches/assignments/responses, versioned date plans/responses, self-reported outcome events, provider transactions/entitlements, device tokens and member-to-waitlist links. Suggested fields include opaque ID, server member/environment IDs, schema/ranking version, created/updated timestamps, revision, state and purpose-appropriate retention. Batch assignments need candidate snapshot/revision, release/expiry and reason provenance; do not store unrestricted copies of private assessments in analytics.

Every profile read/accept must validate assigned-introduction membership, not merely reciprocal eligibility. Existing `accessible_profile` permits eligible profile access outside a new batch concept; hiding cards in the UI alone does not implement scarcity. After blocking, suspension, closure or eligibility change, withdraw inaccessible assignments and deny direct URLs while preserving safe operational audit evidence.

Current feedback booleans default to false. A new outcome model must distinguish absent feedback, unknown attendance, not yet occurred, a negative answer, and an affirmative answer. Do not convert legacy missing data into a negative training label. Keep each member's private notes and feedback inaccessible to their match. An explicit agreement to share second-date interest is a separate action.

## Waitlist-to-member mapping

Do not copy the production waitlist into the app or create dating accounts silently. Link a signup only after a member proves ownership of the relevant verified address or a short-lived single-use claim flow and explicitly chooses dating enrollment. An Apple relay address may differ from the waitlist address; do not merge accounts by a guessed email similarity.

| Waitlist field | Dating mapping |
| --- | --- |
| Opaque signup ID / email lookup | Server-only link after verified claim; not a mobile credential |
| `firstName`, `city` | Optional prefill shown to and editable by the member |
| `ageRange`, `adultConfirmed` | Cannot produce a birth date or verified-age claim; collect dating eligibility afresh |
| `gender`, `genderDescription`, `interestedIn` | Propose a transparent enum mapping and require member confirmation; preserve self-description respectfully |
| `lookingFor` | Confirm the new intent taxonomy rather than silently mapping ambiguous answers |
| Email consent/version/date | Preserve original purpose; not consent to private profile publication, AI processing or all new marketing |
| Source/UTM/referral | Retain bounded attribution for internal analytics; never publish it in member profiles |

The website's personal waitlist data and contact messages are encrypted with existing keys and have 365-day retention. Preserve those keys and policies. Dating data needs a separately documented retention schedule; do not inherit unrelated storage or lifetime defaults accidentally. Leaving dating, deleting a waitlist entry, deleting the whole member account and managing an App Store subscription are distinct user actions with clearly described effects.

## Current web API and unified admin

The waitlist's `lib/waitlist/handlers.ts` is the authoritative existing browser contract: `/api/public/config`, `/api/contact/config`, `POST /api/contact/messages`, `/api/analytics/visit`, `/api/waitlist/signup`, `/status`, `/unsubscribe`, `/delete-request`, and `/delete` (the final four under `/api/waitlist`). Status uses an HttpOnly receipt; unsubscribe/delete signed GETs only review and POSTs mutate.

Owner APIs include `/api/admin/me`, `/overview`, `/signups`, `/export`, `/messages`, `/messages/summary`, `/messages/{id}`, `/messages/{id}/status`, `/emails`, `/emails/preview`, `/emails/test`, `/emails/retry`, campaign preview/send/process and maintenance. Read their actual allowed methods before using them. The email test recipient is fixed to the authenticated owner, not an arbitrary form address.

Contact categories are Privacy, Partnership, Suggestions, Support, Feedback and Other; statuses are new/read/resolved. Contact does not subscribe its sender. The public contact handler requires a same-origin browser request. Do not make the native app spoof a browser Origin to bypass it: implement an authenticated member adapter that reuses validation and writes to the same reviewed inbox, or open the existing contact web page.

Keep one owner experience with linked authoritative data, even if services retain separate physical stores. Extend the protected admin with server-to-server queries for profiles, assignments, reports, dates and entitlements. Put encryption keys, mail keys, storage credentials and provider signing configuration on the server. The mobile client gets only its own safe DTOs. Logs must not contain message bodies, raw access tokens, action tokens, private answers or database exports.
