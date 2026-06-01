# Changelog

All notable changes to this skill will be documented in this file.

## [Unreleased]

### Changed

- Reorganized the repository to use a `skills/teaching-programming/SKILL.md` layout for easier skills.sh-style installation.
- Added a `skills.sh.json` repository configuration file.
- Updated the README to document installation via `npx skills add ... --skill teaching-programming`.

## [0.1.0] - 2026-05-31

### Added

- First public release of the `teaching-programming` skill.
- Runtime contract for small-step teaching during coding sessions.
- Installation guidance for OpenCode, Claude-style folders, AGENTS.md-based tools, and direct path loading.
- Verification prompt and behavior expectations for teaching-mode activation.

### Changed

- Clarified that skill discovery behavior depends on the host agent/runtime.
- Excluded local `.atl/` artifacts from the published repository.
