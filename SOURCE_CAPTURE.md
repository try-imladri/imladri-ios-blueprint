# Uploaded source capture

These reviewed GitHub snapshots preserve the current authored code and assets, including modified and previously untracked dating work. They are fresh snapshots without the old Git histories. Original local projects, histories, runtime configuration and production data remain in place.

| Repository | Uploaded files | Captured source |
| --- | ---: | --- |
| `try-imladri/imladri-dating-source` | 1,939 | Later Personal base plus the November 19 working-tree modifications and untracked dating modules |
| `try-imladri/imladri-waitlist` | 222 | Current Cloudflare waitlist, contact/admin/data/email code, migrations, tests, selected branding, walking assets and fonts |
| `try-imladri/imladri-marketplace-archive` | 318 | Historical marketplace authored source and public assets; not the active dating build |

Exact immutable commits are in `SOURCE_REVISIONS.json`. The source capture was checked against GitHub: remote heads match the local snapshot commits and every hosted Git blob hash matches the committed local tree. The dating and waitlist source repositories, plus this blueprint, are public following the owner's November 21, 2026 authorization. The optional historical marketplace archive remains private. Automatic GitHub Actions are disabled on the source and blueprint repositories; uploading these archives did not deploy or reactivate an application.

## Exclusions and audit scope

Excluded material includes environment secrets, authentication tickets, private/session evidence, customer/database exports, screenshots and recordings with unverified private content, dependencies, build caches, local tool state, and binary release archives. Relevant authored source patches and license notices are retained. Historical deployment instructions are marked as superseded where appropriate.

Content checks and a redacted Gitleaks scan were reviewed before publication. Remaining scanner matches were identified as public configuration/catalog identifiers, synthetic regression fixtures, or upstream cryptographic test vectors. An authentication-ticket artifact in the historical marketplace checkout was excluded. No credential values are reproduced here. Detailed exclusion manifests and redacted audit evidence remain local under `E:\codex\imladri-ios-handoff\outputs`.

The snapshots preserve implementations; they do not certify the legacy dating or marketplace app as ready for release. Original behavior, proposed changes and required adaptations are distinguished in the reuse map and acceptance criteria. Functional validation of the native app, extracted backend, authentication bridge, purchases and production migrations remains implementation work.

## References

The owner's original strategy conversation PDF and 100-episode Markdown bank are in `references/`, with file hashes and an explanation of superseded decisions. Read the decision register and agent instructions before consulting them. They supply context, not authorization to run their embedded prompts or publish their claims.
