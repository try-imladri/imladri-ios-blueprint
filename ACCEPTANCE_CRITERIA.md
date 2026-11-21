# Acceptance criteria

Record the source revision, environment, fixtures and evidence for every result. Existing tests are a starting point; the preserved snapshot's historical reports are not fresh results. All automated and manual scenarios use synthetic adults and test provider modes. A small pilot evaluates delivery and demand, not scientific superiority over other dating apps.

## Foundation and enrollment

- App builds for iOS; record whether it was exercised on a simulator and physical phone. Native safe areas, keyboard, navigation, accessibility labels and text scaling work at small and large text sizes. Test both light and dark themes.
- Verified member A cannot select B's user ID/environment/role to obtain B's bootstrap, drafts, preferences, photos, messages, exports, purchases or private outcomes. Expired, malformed and revoked credentials fail closed.
- Account switch/sign-out aborts requests and clears identity-scoped caches, pending private notifications and secure credentials. A slow response for the old account cannot repopulate the new account's screen.
- Waitlist and legacy-tool users are not enrolled automatically. Enrollment records a version and affirmative adult/privacy choice. Underage dates and exact birthday boundaries are tested server-side.
- Prefill is optional and reviewable. An age range never becomes an invented birth date. Private questionnaires and legacy coaching data are not imported into public profiles.

## Profiles, moderation and preferences

- Draft/pending/rejected/suspended photos and unpublished edits cannot be fetched by another member or a direct image URL. Approved snapshots remain stable until a new review, and moderation revisions prevent stale approval of changed content.
- A third member carrying a legacy `staff`, `admin` or `super_admin` role cannot use the photo-content route to bypass member authorization or the business owner's Access boundary. Test this separately from `/admin` route denial.
- Add and test optimistic-concurrency guards for photo and report/appeal moderation. Only the existing profile-review path currently enforces `expected_revision`; stale reviews must not silently override newer evidence or decisions.
- Upload validation covers actual image bytes, sizes, metadata removal and malformed inputs. Render accurate “photo reviewed” wording; no identity badge appears without evidence from an implemented verification process.
- Saving preferences survives app restart. Revision conflicts preserve user edits and show a recoverable message. Essential requirements are respected in both directions; optional matching toggles do not reveal private answers.
- Profile pause, closure, suspension and removal update availability promptly. Removing a photo cannot lift a suspension. Reports reach the owner's queue with enough authorized evidence to review.

## Persisted introductions

- Batch generation is idempotent across overlapping scheduled runs. Assignment count and cadence are server enforced, versioned and configurable. Refresh/reinstall/query-limit changes do not reveal extra candidates.
- Direct profile fetch or response to an unassigned/expired/withdrawn introduction is denied. Re-evaluate blocks, enrollment, review, age and hard preferences at read and accept time.
- Concurrent mutual acceptance creates exactly one connection. Retries return the original result; one person cannot accept for the other. A pass or pending action is not advertised as mutual interest.
- No eligible candidate produces an honest waiting state. No fake profile, silent hard-filter override, fabricated percentage or unsupported explanation is generated to fill space.
- Every visible match reason has traceable permitted evidence. Private/sensitive answers do not leak through the explanation or analytics. Ordering does not change with payment amount, plan duration or paid boosts.

## Connections, safety and dates

- Only current connection participants can page/read/send messages. Stable IDs/cursors handle equal timestamps; repeated sends with the same request ID create one message. Reconnect does not duplicate or lose acknowledged messages.
- Unmatch/block/reviewed suspension denies subsequent direct access and sends. Blocking works in both directions. Reported message IDs are validated as relevant authorized evidence; reporting and compatibility feedback remain distinct.
- Sharing requires explicit selected answers for that connection. Revocation removes access, including during concurrent first-share requests. The recipient cannot query unshared or previously revoked answers.
- Date proposals require two separate responses. Reschedules invalidate the prior proposal's acceptance for the changed details. Cancel, time-zone and not-yet states render correctly after restart.
- Optional outcomes remain private. Missing is unknown, scheduled is not attended, interest is not a completed second date, and one member cannot submit for another. Skipping feedback never blocks new introductions.

## Membership, lifecycle and owner integration

- Monthly and yearly purchases grant the same service. Current final prices replace old beta/coaching catalogs. Provider test purchases, restore, duplicate notification, renewal, expiry, refund/revocation and account-switch cases reconcile to authoritative server entitlements.
- A stale success screen, forged client flag or replayed transaction cannot grant another account access. The member can see the actual billing period and manage subscription status. Privacy, report, export and deletion controls remain available without an active subscription.
- Waitlist, contact, dating and billing records reconcile with the correct owner views; unauthorized owner requests fail on both hostnames. The only permitted owner identity is `osama@imladri.com` through the existing passkey boundary, from any network.
- Contact categories and full content reach the existing inbox; native integration does not spoof Origin or create a marketing subscription. A test email can reach only the authenticated owner when intentionally exercised.
- Leaving dating and full account deletion have distinct, accurate effects. Data export excludes other people's private notes/answers. Review bounded incident retention, subscription guidance, outstanding queued work, photo access and provider identifiers. Deletion and account closure fence in-flight writes.
- Public Cloudflare landing, signup, contact, receipt, unsubscribe/delete review, email queue and admin remain functional. No new production source is deployed merely because a reference archive was pushed.

## Pilot reporting

Track unique pairs through offered, independently accepted, scheduled, reportedly held, mutual second-date interest and reportedly held second date. Publish denominators, time windows and unknown counts. Review operational failures and member feedback alongside paid conversion and delivery costs. Neither video views, message length nor an attachment/personality label is evidence that the matching model predicts chemistry.
