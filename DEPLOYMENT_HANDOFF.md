# Environment, build and deployment handoff

## Source and environment setup

Clone the blueprint and the two source snapshots through the owner's authorized private GitHub access. Pin the listed source revisions and record all adapted files. Keep the legacy archive unchanged as a reference; implement in a new app workspace. Preserve the existing Cloudflare production deployment and encryption/signing keys. New repository pushes are backups/handoffs, not authorization to reactivate old Emergent, Render or Cloudflare projects.

Create separate local/test, pilot/staging and production configuration. Use synthetic fixtures and provider test modes in development. A staged backend must enforce its own environment on every database read/write, scheduled batch and provider callback. Never copy the production D1 dataset, private legacy database, real photos or customer messages into test fixtures or GitHub.

Document configuration **names and purpose**, not secret values. Member API origin/auth audience/issuer, database binding, protected object storage, mail sender, push credentials, purchase signing/provider notification settings and batch schedule belong in environment-specific configuration. Server secrets never go into mobile bundles. The waitlist already requires its data/signing/mail secrets; preserve these while records exist and do not substitute generated keys on deployment.

## Build and schema process

Commit a versioned OpenAPI contract and native client types. Define explicit migrations for new batch, plan, outcome, purchase and identity-link stores, plus unique indexes/idempotency constraints and rollback compatibility. Test migrations against empty and representative synthetic prior schemas. Do not modify historical applied migrations or replay initialization against a live store.

For the current waitlist snapshot, inspect its `package.json` and README for `npm run build`, the Cloudflare configuration, TypeScript check, and `node --test tests/backend.test.mjs tests/access.test.mjs tests/mail-template.test.mjs`. Run only checks relevant to changed code; use synthetic transport for mail tests. For dating, inspect Python dependencies and the three dating regression suites linked in `REUSE_MAP.md`, and run them against the selected storage adapter. Avoid launching the entire legacy product merely to exercise the extracted domain.

For iOS, follow current [Expo build guidance](https://docs.expo.dev/build/introduction/) if that stack is chosen, or the chosen native toolchain's official instructions. Record bundle identifier, build number, dependency lockfiles, signing owner, supported iOS versions, entitlements and provider test mode. A Windows source build is not proof of iOS behavior; produce installable iOS evidence through a supported Mac or cloud build path and test device/simulator behavior honestly.

## Release record

Each candidate release records app/backend revisions, schema/contract versions, target environment, acceptance results, device evidence, known limitations and an operational rollback procedure. Exercise retry/background work, duplicate callbacks and scheduled batch overlap before opening a cohort. Monitor availability, queue failures, authorization errors, billing reconciliation and incident response without logging message bodies, private answers, access tokens or signed action URLs.

Keep public availability truthful. App Review needs a functional service path and appropriate reviewer access; never supply the production owner's admin credential as an app demo account. Review the current [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/) for user-generated content, privacy/account deletion, login and payment rules. Credential creation, signing agreements, device verification and financial actions follow the applicable user/tool handoff rules. Record actual completion rather than treating a requested action as a successful release.
