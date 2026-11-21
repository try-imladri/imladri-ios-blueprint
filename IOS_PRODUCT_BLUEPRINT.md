# Product blueprint

## Promise and scope

Build a calm introduction service: a few relevant people, clear reasons to consider each person, and mutual choice about what happens next. Payment purchases the same complete service for every member; it never purchases another person's attention, superior ranking, or privileged access to private answers. Do not advertise guaranteed attraction or relationship outcomes.

The public waitlist remains open to adults from every city, with no demographic quotas or signup caps. Operational availability of introductions is a separate state from the ability to register interest. Select a pilot using actual mutual candidate coverage, participant readiness, and support capacity. Do not convert a crude gender ratio into a public admission restriction or invent members to fill an empty city.

## Main navigation

Use four main areas: **Introductions, Connections, Dates, Profile**. Onboarding and membership settings sit outside or within these flows, not as additional competing bottom tabs.

### Onboarding and Your Type

1. Authenticate with a supported member identity flow. Show account recovery and explicit session state.
2. Explain dating participation separately from the waitlist or prior Imladri tools. Record adult confirmation and a versioned enrollment notice.
3. Gather a display name, date of birth for adult eligibility, gender, city, relationship intent/structure, bio, and appropriate photos. Display age to eligible members, not raw birth date or exact address.
4. Let the member preview what will be visible and submit it for moderation. Draft, pending, approved, rejected, paused, and suspended states need distinct explanations and next actions.
5. Offer a short staged preference intake with saved progress. Separate what a person says about themselves from what they prefer in a partner. Mark preferences versus essential requirements. Private answers, use for matching, and sharing with one connection are separate choices.

The legacy catalog is reusable wording and a starting schema; it is not a validated measure of chemistry. Do not require the entire older Your Type catalog or a fixed 60–90 item assessment simply to join the waitlist. Test intake completion and usefulness with actual pilot participants. Any genuine identity/age verification system needs a defined provider, evidence state, consent and retention design. Until implemented, display accurate photo/profile-review language.

### Introductions

Show an assigned weekly set of complete profile cards with readable reasons and clear accept/pass actions. The exact batch size and expiry policy are decisions to record before release; keep them server-configurable. Persist assignment and exposure state so refreshing, reinstalling, changing a client query limit, or calling the API directly cannot retrieve an unlimited deck.

Eligibility must be reciprocal and rechecked when displaying or accepting an introduction: active explicit enrollment; adult eligibility; published approved profile/photos; both people's allowed genders, age ranges, geography, intentions and essential requirements; no blocks, suspension or closure. Never relax hard requirements to make the screen look populated.

The legacy `preference_score` counts stated acceptable answers. Keep it explainable and versioned if reused. A reason must be supported by fields both users permitted for that purpose. Private intimacy answers cannot leak through explanation text. Do not display invented compatibility percentages, attachment diagnoses, or claims that an LLM knows hidden intentions.

States include: complete profile, awaiting review, waiting for local availability, no eligible introduction this cycle, introduction available, accepted by me, mutual connection, declined, expired, and withdrawn. Empty states tell the truth and offer useful profile/support actions. Privacy controls and deletion remain available without a paid subscription.

### Connections and messaging

Open a connection only after both people accept a valid assigned introduction. Messages belong to that connection and require current participant authorization on every page, send, photo request, and sharing action. Preserve idempotent sends, stable ordering/cursors, unread state, cancellation of stale requests, and clearing cached data on sign-out/account switch.

Offer unmatch, block, report and accessible support. A block revokes server-authorized access in both directions, including direct API/photo requests. Clear the client's relevant cached content on a best-effort basis; the service cannot guarantee erasure of images somebody already copied. A safety report is a different workflow from “not a romantic fit.” Do not turn member feedback into public scores. Push notifications are optional, can be disabled, and should not expose sensitive message or questionnaire content on a locked screen by default.

### Dates and private follow-up

The Dates area is new work. Start with a simple proposed plan attached to an active mutual connection: time, public venue/place description, proposer, and each member's response. A reschedule creates a new proposal that requires agreement; one person's edit must not become the other person's acceptance. Time-zone display, cancellation and unknown status require explicit handling.

Afterward offer a brief optional check-in: did they meet, would they like another date, and any private note. Distinguish one person's report from mutually confirmed attendance, second-date interest from an actual second date, and a scheduled plan from a completed meeting. Missing feedback remains unknown. Do not block introductions for silence or infer a relationship from inactivity or message latency.

Free-form venue suggestions can be useful without a partnership business. Main Event, Puttshack and cinema examples in the strategy document are not signed partners. Discounts, sponsorships, booking fees and paid listings stay out of the initial promises until real agreements and user benefit exist.

### Profile, membership and data controls

Members can edit their own information, preview the public profile, change preferences, pause new introductions, review blocked accounts, manage notifications, contact support, export appropriate data, leave dating, and delete their account. Explain the difference between pausing introductions, canceling renewal, leaving dating, and deleting the entire account. Do not claim one automatically performs all four.

Final commercial intent is one US plan: **$24.99/month or $249.99/year**, with equal functional entitlements. Display the real storefront localized price and billing period supplied by the billing provider. The annual price is about $20.83/month equivalent and saves $49.89 against twelve monthly payments; avoid the mathematically inexact “exactly two months free” claim.

Implement native purchases, restore, renewal/cancellation/expiry/refund/revocation and server-side entitlement reconciliation. StoreKit is the proposed iOS purchase adapter; review current storefront rules before selecting any external purchase flow. A client boolean or old web checkout return URL cannot grant service. Annual cash receipts are not monthly recurring revenue or proof of profitable delivery. Do not reuse the old $19 beta metadata, free-beta assumptions, reply-credit catalog or historical premium tiers as current billing.

## Shared owner operations

The owner dashboard remains a protected web application. Extend its navigation with dating profile/photo review, introduction batches, connection/date health, reports and appeals, and subscription reconciliation status. Preserve the existing waitlist, email outbox/campaign preview and six-category contact inbox.

Show records with useful IDs, timestamps, state, reason and the correct scope. Avoid a dashboard that merely displays client events while authoritative records live elsewhere. Counts must reconcile to stored records, identify their denominator/window, and never infer romantic outcomes from engagement. Access to sensitive incident evidence should be limited to what the owner needs to resolve it and recorded in an audit trail.

## Implementation phases

| Phase | Deliverable | Exit evidence |
| --- | --- | --- |
| Foundation | Native shell, identity, API adapter, synthetic environments, design assets | Member isolation and real iOS build evidence |
| Profile slice | Explicit enrollment, staged preferences, photo/profile review, owner queue | Two reviewed synthetic profiles; draft/private fields cannot leak |
| Introduction slice | Persisted assignment, reciprocal eligibility, supported reasons and mutual acceptance | Refresh/bypass/concurrent-accept tests; honest no-candidate state |
| Connection slice | Messaging, unmatch/block/report, native lifecycle handling | Multi-user and reconnect tests plus moderation evidence |
| Service slice | Simple date proposals, optional outcomes, purchases/restore and owner reconciliation | Full journey and entitlement lifecycle tests |
| Pilot release | Usable cohort, support/incident handling, account/data controls, actual device QA | Acceptance document passes with named limitations |

New Year momentum is a recruitment opportunity, not evidence that a fixed date is safe to promise. Each phase needs demonstrated behavior. Defer sophisticated learned ranking, automatic venue booking, social feeds, coaching, unlimited discovery and public popularity metrics until the introduction service provides evidence that they solve a real problem.

## Design assets

Use the latest two-face transparent logo and the IMLADRI name beside it. The website's headline/wordmark font is Barlow Condensed Black; body font assets are Plus Jakarta Sans. Preserve their font-license files. Adapt spacing and interactions for iOS, Dynamic Type, safe areas, keyboard behavior, contrast and reduced motion. The walking silhouettes may be used as an optional branded onboarding moment, not an obstruction to sign-in, accessibility or first meaningful content. Light and dark themes need real device screenshots; do not reuse an obsolete emblem or AI-security social metadata.
