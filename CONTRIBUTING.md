# Contributing

Thanks for your interest in improving Liquid Glass.

## Reporting Issues

Use the [issue templates](.github/ISSUE_TEMPLATE/). Include:

- Home Assistant version
- HACS version
- Browser & version
- Screenshot when relevant

## Submitting Changes

1. Fork the repo
2. Create a feature branch (`git checkout -b feat/your-change`)
3. Use [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, `style:`, `refactor:`, `chore:`)
4. Update `CHANGELOG.md` under `[Unreleased]`
5. Push and open a Pull Request

## Style Guide

- YAML: 2-space indent, no trailing whitespace
- Color values: lowercase hex or `rgba()` notation
- Group related variables under `# ----- SECTION -----` comments
- Test changes against common Lovelace cards (entities, glance, button, picture-elements)

## Versioning

We follow [Semantic Versioning](https://semver.org/):

- `patch` (`v1.0.x`) — bug fixes, minor color tweaks
- `minor` (`v1.x.0`) — new variables, backward-compatible additions
- `major` (`vX.0.0`) — breaking changes, redesigns

## Release Process

1. Bump version in `CHANGELOG.md` (move `[Unreleased]` → new version section)
2. Commit & push to `main`
3. Create a GitHub Release with matching tag (`vX.Y.Z`)
4. HACS will pick up the new release automatically
