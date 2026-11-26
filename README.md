# prunely-releases

Fallback download host for Prunely updates (owner decision D1, PRUN-522). The primary host is
`https://updates.prunely.io`. This repository holds **releases only**: no code, no issues.

- One release per stable version, tag `v<version>`, never a pre-release.
- Each release carries the installers, `latest.json` and `latest.json.sig`. The manifest is signed
  with the Prunely update key (repository `azara-labs/release-signing`); the app refuses any file
  whose signature or SHA-256 does not match.
- The app reads `https://github.com/azara-labs/prunely-releases/releases/latest/download/latest.json`
  only when the primary host cannot be reached.
- A published file is never replaced.
- Rollback: on both hosts in the same step. Put the previous `latest.json` back on the primary host
  and mark the previous release here as latest; otherwise clients that cannot reach the primary
  are still offered the withdrawn version. Full procedure: `azara-labs/release-signing` README,
  "Roll back a release".
