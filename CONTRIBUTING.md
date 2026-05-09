# Contributing

Thanks for your interest in improving Liquid Glass.

## Reporting Issues

Use the [issue templates](.github/ISSUE_TEMPLATE/). Include:

- Home Assistant version
- HACS version
- Browser & version
- Screenshot when relevant

## Diagnosing color / white-on-white / unreadable text bugs

HA's frontend renders form controls and dialogs through several token generations (see [README — Architecture](README.md#architecture--token-layers)). Before opening an issue:

1. Open the affected element in DevTools → **Elements** tab
2. Expand `#shadow-root (open)` chains until you reach the actual `<input>`, `<wa-input>`, `<ha-combo-box-item>` or similar
3. **Computed** tab → identify the CSS variable resolving the wrong color (e.g. `color: var(--md-list-item-label-text-color, #1d1b20)`)
4. **Styles** tab → confirm which rule is winning, which selector
5. Include in the issue:
   - The element tag (e.g. `<wa-input>` inside `<ha-input>`)
   - The relevant CSS variable name(s)
   - What color it currently resolves to vs. what's expected
   - Screenshot of the Computed/Styles panel

This prevents the speculative-fix-stacking pattern that hit v1.2.2 → v1.2.3 → v1.2.4 (each release added more tokens without identifying root cause).

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
