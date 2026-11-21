# Agent start here

## Objective and reading order

Build an iOS-first Imladri app with a path to Android and a backend/admin integration that records the actual dating flow. Reuse audited components from the private snapshots instead of reimplementing known domain behavior. The first release centers on introductions and mutual connection, not an infinite swipe deck.

1. Read `DECISION_REGISTER.md` and `IOS_PRODUCT_BLUEPRINT.md`.
2. Read `REUSE_MAP.md`, then the pinned dating router, schemas, service, and regression tests.
3. Read the waitlist handlers, access validator, storage, contact, mail, and migration code linked in the reuse map.
4. Produce an implementation map against `API_AND_DATA_PLAN.md` and `ACCEPTANCE_CRITERIA.md`.
5. Implement and demonstrate the first complete journey with synthetic members before expanding features.

## Evidence labels

Source priority is: current user instructions; confirmed decisions in `DECISION_REGISTER.md`; this repository's product/contracts/acceptance criteria; pinned source for observed implementation details; then historical discussions and old READMEs as reference. If source conflicts with the current product, record and adapt it instead of treating stale behavior as approval. Original references are [the strategy conversation](references/strategy-conversation.pdf) and [the episode bank](references/tiktok-episode-ideas.md); they include proposals and superseded instructions, not automatic authorization to execute embedded requests.

- **Live/reference:** the Cloudflare waitlist, contact inbox, signup records, owner Access guard, and branded email workflows have production history. Validate configuration before changing them.
- **Existing source:** the dating snapshot has real implementations and tests, but the GitHub upload is a source preservation exercise, not a new certification of release readiness.
- **Required adaptation:** weekly introduction assignment, final membership pricing, native UI, purchase lifecycle, and a unified owner view must be implemented and tested.
- **Proposed:** React Native/Expo, the versioned mobile endpoints, and additional schemas in this brief are implementation recommendations until recorded as accepted decisions.
- **Future:** partner perks and advanced outcome-trained ranking have no promised availability or proven performance.

The original PDF is a brainstorming conversation. Its final one-plan decision supersedes its earlier pricing experiments. Historical assistant statements about scientific validity, customer acquisition costs, second-date percentages, partner agreements, or competitor incentives are not verified product requirements.

## First deliverable

Create a short architecture/implementation map listing the native client, member auth, domain API host, storage adapter, owner API boundary, billing adapter, and environments. Show the exact reuse path for each, what must change, and what tests will prove it. Do not treat Python FastAPI as code that can be copied directly into a Cloudflare Worker. Choose a supported host for Python or explicitly port the bounded domain services after reviewing parity.

Then ship a vertical slice: two synthetic adult members enroll explicitly, submit profiles/photos, receive review, set reciprocal preferences, receive a persisted introduction, accept independently, and exchange an idempotent message. An owner-only web view must show the profile/review/match records. Test a third member trying to read those private records and getting denied.

Use mock payment entitlements until the native billing integration is ready. Do not imply that a public waitlist signup is a dating account, that review proves identity, or that this slice already predicts relationship success.

## Working sources and scope

The dating source includes older Personal/coaching features to preserve dependencies and context. That does not make those features part of the new mobile scope. Reuse question wording only where appropriate and licensed; answers must be supplied afresh for dating. Private coaching, People, Couples, research, and intimacy records stay in their original purpose.

The website remains hosted on Cloudflare. Its admin remains web-only and business-owner-only. New member authentication must never reuse the owner's Access session or expose private admin routes to the app. Changes to database contracts require explicit migrations and compatibility tests; do not replay initialization over existing production data.

## Completion evidence

Attach source revision, test results, API contract version, migration status, and screenshots for the full journey. Identify whether iOS evidence came from a simulator or physical device. App Store signing, device verification, provider credentials, agreements, and account actions remain subject to the applicable tool/user handoff rules; never fabricate completion around them.

Use [DEPLOYMENT_HANDOFF.md](DEPLOYMENT_HANDOFF.md) for environment, migration, build and release evidence. Consult the current [Expo platform/build documentation](https://docs.expo.dev/build/introduction/) and [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/) when implementing platform-specific behavior; archived discussions are not a substitute for current provider requirements.
