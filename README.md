# Imladri iOS implementation blueprint

This is the entry point for the coding agent building Imladri's iOS-first dating app. Read [AGENT_START_HERE.md](AGENT_START_HERE.md), then the product, reuse, API/data, acceptance, and decision documents below. This repository specifies a build; it is not evidence that the app is already released.

| Document | Purpose |
| --- | --- |
| [Public access](PUBLIC_ACCESS.md) | Token-free reading/cloning and optional archive boundaries |
| [Agent start](AGENT_START_HERE.md) | Reading order, first deliverable, source priority, and boundaries |
| [Product blueprint](IOS_PRODUCT_BLUEPRINT.md) | Screens, flows, matching behavior, membership, and delivery phases |
| [Reuse map](REUSE_MAP.md) | Exact files to inspect, reuse, adapt, or retire |
| [API and data plan](API_AND_DATA_PLAN.md) | Existing endpoints versus proposed mobile contracts and shared admin integration |
| [Acceptance criteria](ACCEPTANCE_CRITERIA.md) | Observable tests for each milestone and release |
| [Decision register](DECISION_REGISTER.md) | Confirmed decisions, implementation proposals, and unresolved choices |
| [Deployment handoff](DEPLOYMENT_HANDOFF.md) | Environment boundaries, contracts/migrations, iOS builds, and release evidence |
| [Pinned source revisions](SOURCE_REVISIONS.json) | Machine-readable source repositories and immutable commit IDs |
| [Source capture](SOURCE_CAPTURE.md) | What was uploaded, what was intentionally excluded, and verification scope |
| [Original references](references/README.md) | Historical strategy PDF and TikTok episode bank, with source-priority guidance |

## Connected source repositories

- [Dating source snapshot](https://github.com/try-imladri/imladri-dating-source): the later Personal code plus the previously uncommitted November 19 dating work. Inspect its provenance and sanitization notes. Source pin: `5b9100518d3942c969bc87f8ad46a924e92d7312`.
- [Current waitlist](https://github.com/try-imladri/imladri-waitlist): public Cloudflare landing, signup, contact, encrypted storage, branded email, and owner dashboard. Source pin: `fd8b5b8c28d3a155eb160ad80ffe6e749f768101`.
- [Older marketplace archive](https://github.com/try-imladri/imladri-marketplace-archive): optional private historical reference, not a dependency of the iOS build. Its earlier product and deployment instructions are superseded; skip it if you do not have access.
- [Older Personal repository](https://github.com/try-imladri/imladri-personal): optional private historical baseline; the public dating snapshot already preserves the newer code needed for reuse.
- [Earlier AI-security repository](https://github.com/try-imladri/imladri): optional private retired-product reference, not a build dependency. Do not restore its product copy, routes, or deployment as part of this build.

The clean source snapshots intentionally omit runtime secrets, customer data, environment state, recordings, and local reports. Provision runtime configuration separately; a missing secret is not a reason to disable verification. The blueprint, dating source and current waitlist are public and require no GitHub token for reading or cloning. Historical private archives are optional; see [PUBLIC_ACCESS.md](PUBLIC_ACCESS.md).

## Product in one sentence

Imladri offers a few thoughtful dating introductions, clear reasons grounded in members' stated information, one complete membership, and no paid ranking or visibility boosts.

The first successful implementation is a real, tested journey: adult member enrolls, creates a reviewed profile, sets mutual preferences, receives an assigned introduction, both members accept, they exchange messages, and optional date feedback appears only in the correct private views. The owner can review the relevant operations from a protected web dashboard. Build that journey before adding a venue marketplace or complex AI ranking.

Reviewed date: November 20, 2026. Original strategy discussion's final pricing decision is one plan at **US $24.99/month or $249.99/year**. Earlier $19 dating beta copy, coaching reply credits, premium tiers, gender pricing, and $349 reset offers are historical and must not become current app entitlements.

Pinned repository revisions and capture scope: [SOURCE_REVISIONS.json](SOURCE_REVISIONS.json). Original owner-provided documents: [historical references](references/README.md).
