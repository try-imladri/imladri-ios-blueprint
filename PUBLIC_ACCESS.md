# Public source access

On November 21, 2026 the owner authorized public read access so the coding agent can inspect and adapt the app without private-repository credentials.

The complete required build inputs are public:

- https://github.com/try-imladri/imladri-ios-blueprint
- https://github.com/try-imladri/imladri-dating-source
- https://github.com/try-imladri/imladri-waitlist

Read `AGENTS.md` and `AGENT_START_HERE.md`, then follow the exact source revisions in `SOURCE_REVISIONS.json` and file links in `REUSE_MAP.md`. No GitHub token or account is required to read or clone these public inputs. If a tool cannot open a GitHub HTML page, use the repository's raw file URL or clone the public repository.

The marketplace archive, older Personal repository and retired AI-security repository remain optional historical references and may remain private. They are not dependencies of the first iOS implementation slice. Do not stop the build or request credentials solely to read one of those archives.

Public read access does not grant write access to the owner's repositories. The agent can adapt a local checkout, fork the public source where supported, or propose changes. Pushing to the owner's branches still requires the owner's authorized GitHub access.

The live website, member/private records and owner dashboard are separate from source visibility. Preserve the existing authentication and runtime-secret boundaries. GitHub Actions remain disabled; publication is not a deployment.

Public source can be copied by anyone. A later visibility change does not recall copies already downloaded.
