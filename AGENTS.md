# AGENTS.md

## Project

Quire for iOS: the native iPhone client for Quire, a self-hosted study workspace (courses, lecture/recitation decks,
documents, notes, AI chat). It talks to the Quire web app (`EzraGubbay/quire`, `apps/web`) only through the versioned
mobile API (`/api/mobile/v1`) — the same contract and fixtures the Android app uses.

Initiative: **QMOB — Quire Mobile** (GitHub Project 3).

**Status: frozen until Android v1.1.0 ships.** Android (`EzraGubbay/quire-android`) is strictly first: implemented,
tested, released. Until the human reopens "iOS Sprint 1", do not implement anything here; every epic is `needs-spec`.

The one thing that must never break: the user can open a course and read a file, including offline once downloaded.

## Scope: reader-first (mirrors Android, minus push)

In scope: pairing, browsing courses / sessions / files with type labels, PDF and deck viewing, downloads, reading
notes, AI chat with streaming, background sync and upload.

Not in scope: **push notifications (APNs)**, writing or editing notes, annotations, mind-map, homework/test modules,
iPad-specific layouts.

UI must be **iOS-native and aesthetic** (NavigationStack, TabView, Dynamic Type, dark mode, VoiceOver, RTL-safe). It is
neither a shrunk web UI nor a port of the Android layouts — reuse the behaviour and acceptance journeys, not the UI.

## Stack

- **Native only: Swift + SwiftUI.** No React Native, Flutter, KMP, or web wrappers.
- Platform frameworks first: URLSession (incl. background sessions), PDFKit, Keychain, BGTaskScheduler.
- Persistence choice (SwiftData vs GRDB), deployment target and bundle id are decided in QMOB-iE0.

## Commands

No Xcode project exists yet (created by QMOB-iE0). **Intended** commands, to be confirmed and corrected by that epic:

- Build: `xcodebuild build -scheme Quire -destination 'platform=iOS Simulator,name=iPhone 16'`
- Lint: `swiftlint --strict`
- Unit tests: `xcodebuild test -scheme Quire -only-testing:QuireTests -destination 'platform=iOS Simulator,name=iPhone 16'`
- UI / e2e tests: `xcodebuild test -scheme Quire -only-testing:QuireUITests -destination 'platform=iOS Simulator,name=iPhone 16'`

CI for iOS is specified first in QMOB-iE0 (`docs/CI-SPEC.md`, macOS runners), then implemented — same order as Android.

## Branches and merging — hard rules

```
agent/<issue>-<slug>  ──PR──▶  dev-rc  ──release PR──▶  main  ──tag v<version>──▶  release
```

- Every change is a feature branch + pull request **into `dev-rc`**. Never commit or push to `dev-rc` or `main`.
- **Nothing merges into `dev-rc` unless unit tests (and build + lint) pass.**
- **Nothing merges into `main` unless CI and e2e (UI tests) pass.** `dev-rc` → `main` only as a release PR when
  shippable — one sprint = one release.
- Agents never merge. Only the human merges, tags and releases.
- Do not weaken, skip or delete a test or a check to get green.

## Test-driven development

- **Per user story:** unit tests are defined first and committed failing, then the implementation.
- **Per epic:** the epic's UI-test journey is written before its stories (skipped with a `QMOB-iE<n>` marker), each
  story un-skips what it satisfies, and the epic is done when none remain.
- Network code is tested against the shared contract fixtures (`docs/api/fixtures/mobile-v1/` in `EzraGubbay/quire`).

## Working rules

- Work only on the issue you were given: **one issue, one branch, one PR, one implementer.**
- Only pick up issues labelled `agent-ready` in the currently **open** milestone with no open blockers. Skip
  `human-only` and `needs-spec`.
- Branch name: `agent/<issue-number>-<short-slug>`. Open PRs as drafts into `dev-rc`; the body says `Closes #<n>` and
  ticks each acceptance criterion.
- If acceptance criteria are ambiguous, comment on the issue with your question and stop.
- Stay inside the issue's "Where to work". No drive-by refactors, reformatting or renames.
- Never edit `.github/` (workflows, CODEOWNERS), secrets, signing or CI configuration.
- Write `@attributes` and other `@words` in backticks in issues, PRs and comments so GitHub does not notify people.

## Secrets

Never create, read, print or commit secrets: signing certificates, provisioning profiles, App Store Connect keys,
device tokens, GitHub tokens. Their setup is human-only.

## Definition of done

- Every acceptance criterion is ticked in the PR body; tests were written first and are in the PR.
- The issue's verification command passes; required checks are green.
- No changes outside the issue's scope.

## Planning structure

- Epic (parent issue, type Feature, label `epic`) → User story (sub-issue, label `story`, size XS–M) → Tasks.
- Sprints are milestones; one sprint = one release. Plan: `docs/BACKLOG.md`.
- Labels: `agent-ready`, `needs-spec`, `human-only`, `spike`, `agent:claude`, `agent:gemini`, `epic`, `story`, `task`,
  `ios`.
