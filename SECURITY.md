# Security Policy

## Supported Versions

Only the latest minor release line is actively maintained. Older minor releases do not receive patches.

| Version | Status        |
|---------|---------------|
| 1.3.x   | ✅ Supported  |
| < 1.3   | ❌ End of life |

## Reporting a Vulnerability

This repository is a Home Assistant frontend theme — no backend, no user data, no authentication code. The realistic security surface is narrow:

- Malicious YAML/CSS injection via theme tokens (very narrow vector — themes are user-installed)
- Supply-chain risks in the GitHub Actions used by CI workflows (continuously tracked by Dependabot)

If you find a vulnerability nonetheless, please use **GitHub Private Vulnerability Reporting** rather than a public issue:

1. Open the [Security tab](https://github.com/studio-prisma/homeassistant-theme-liquid-glass/security)
2. Click **Report a vulnerability**
3. Include a clear description and reproduction steps

You will get a first response within **14 days**. Resolution timeline is best-effort — this is a hobby project maintained by a single person.

## Out of Scope

- Issues that only affect a non-supported (older) version
- Cosmetic / accessibility / contrast issues without security impact — use the public [Issues tracker](https://github.com/studio-prisma/homeassistant-theme-liquid-glass/issues) instead
- Vulnerabilities in dependencies that are already auto-tracked by Dependabot — no separate report needed

## Code Scanning

Static code analysis (CodeQL or similar) is **intentionally not enabled** for this repository. The codebase consists of YAML and Markdown only — no executable program logic to analyze. Supply-chain hygiene for GitHub Actions is covered by Dependabot. This is a deliberate maintainer decision, not an oversight.

## Disclosure

Once a fix is merged and a release is published, the affected version will be referenced in the [CHANGELOG](CHANGELOG.md) and the corresponding GitHub Release notes. Reporters who wish to be credited will be acknowledged in the release notes.
