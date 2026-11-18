# QMOB backlog — Quire for iOS (after Android)

**Status: planned, not started.** Android (`EzraGubbay/quire-android`) ships completely first — through v1.1.0.
The full Android backlog, whose stories the iOS ones mirror, is in
[quire-android/docs/BACKLOG.md](https://github.com/EzraGubbay/quire-android/blob/main/docs/BACKLOG.md).

- The mobile API layer (QMOB-E1, `/api/mobile/v1` in `EzraGubbay/quire`) is shared — no iOS API epic.
- **No push notifications on iOS.**
- Native Swift + SwiftUI; same rules: epic → user story → tasks, 1 story = 1 PR, TDD, feature → `dev-rc` → `main`.
- At iOS kickoff: write each planned story as a sub-issue (Goal, acceptance criteria, verification command, where to work, out of scope, Size XS–M), starting with iE0 whose first deliverable is the iOS CI specification.

## Epics

| Epic | Issue | Mirrors Android | Title | Sprint |
|---|---|---|---|---|
| iE0 | [#1](https://github.com/EzraGubbay/quire-ios/issues/1) | E0 (quire-android#1) | Repo scaffold + CI/CD pipeline (Xcode, SwiftLint, XCTest, XCUITest) | iOS Sprint 1 — Scaffold, Shell & Sign-in (v0.1.0) |
| iE2 | [#2](https://github.com/EzraGubbay/quire-ios/issues/2) | E2 (quire-android#3) | App shell: navigation + iOS-native design system | iOS Sprint 1 — Scaffold, Shell & Sign-in (v0.1.0) |
| iE3 | [#3](https://github.com/EzraGubbay/quire-ios/issues/3) | E3 (quire-android#4) | Auth: device pairing against the mobile API | iOS Sprint 1 — Scaffold, Shell & Sign-in (v0.1.0) |
| iE4 | [#4](https://github.com/EzraGubbay/quire-ios/issues/4) | E4 (quire-android#5) | Course & file browser (reader) with type labels | iOS Sprint 2 — Browse & Read (v0.2.0) |
| iE5 | [#5](https://github.com/EzraGubbay/quire-ios/issues/5) | E5 (quire-android#6) | Document viewer (PDFKit) + downloads | iOS Sprint 2 — Browse & Read (v0.2.0) |
| iE6 | [#6](https://github.com/EzraGubbay/quire-ios/issues/6) | E6 (quire-android#7) | AI chat (streaming) | iOS Sprint 3 — AI Chat (v0.3.0) |
| iE7 | [#7](https://github.com/EzraGubbay/quire-ios/issues/7) | E7 (quire-android#8) | Background upload / sync | iOS Sprint 4 — Sync & Release (v1.0.0) |
| iE9 | [#8](https://github.com/EzraGubbay/quire-ios/issues/8) | E9 (quire-android#10) | Release: signing + distribution | iOS Sprint 4 — Sync & Release (v1.0.0) |

## iE0 — Repo scaffold + CI/CD pipeline (Xcode, SwiftLint, XCTest, XCUITest) ([#1](https://github.com/EzraGubbay/quire-ios/issues/1))

A buildable Swift + SwiftUI project with CI (build, SwiftLint, unit tests, UI tests on a simulator) and the same `dev-rc` / `main` hard rules as Android.

Planned stories:
- Xcode project scaffold (SwiftUI app, bundle id, deployment target)
- SwiftLint + SwiftFormat
- XCUITest harness with a stubbed URLProtocol server + contract fixtures
- CI workflow on macOS runners (spec first: `docs/CI-SPEC.md`)
- Branch rulesets (human)
- Versioning

## iE2 — App shell: navigation + iOS-native design system ([#2](https://github.com/EzraGubbay/quire-ios/issues/2))

A SwiftUI shell that feels native on iPhone (TabView, NavigationStack, Dynamic Type, dark mode) sharing Quire's palette — not a port of the Android or web layout.

Planned stories:
- e2e journey first
- Design tokens + theme
- Tab + navigation scaffold
- Component kit
- Snapshot tests
- Settings (appearance)
- App icon + launch screen (needs asset)

## iE3 — Auth: device pairing against the mobile API ([#3](https://github.com/EzraGubbay/quire-ios/issues/3))

Pair by QR or code against `/api/mobile/v1`, token in the Keychain, 401 returns to pairing.

Planned stories:
- e2e journey first
- API client + error mapping + contract tests
- Keychain session storage
- Pair screen (manual)
- QR scan + `quire://pair` URL scheme
- Session expiry + sign-out

## iE4 — Course & file browser (reader) with type labels ([#4](https://github.com/EzraGubbay/quire-ios/issues/4))

Offline-first course, session, file and notes lists with type labels, filters and search.

Planned stories:
- e2e journey first
- Persistence + repositories (SwiftData/GRDB — decide in iE0)
- Courses list
- Course screen (Sessions · Files · Notes)
- Files filters/sort
- Search

## iE5 — Document viewer (PDFKit) + downloads ([#5](https://github.com/EzraGubbay/quire-ios/issues/5))

PDFKit-based viewer with resume position and reliable background downloads (URLSession background configuration).

Planned stories:
- e2e journey first
- Download engine (background URLSession, resume data, ETag)
- PDF viewer
- Open-file flow + Quick Look for originals
- Downloads library
- Share sheet / save to Files
- Notes reader (reuse ADR 0001 conclusions)

## iE6 — AI chat (streaming) ([#6](https://github.com/EzraGubbay/quire-ios/issues/6))

Streaming chat over the NDJSON endpoint with citations that open the viewer at the page.

Planned stories:
- e2e journey first
- NDJSON stream → AsyncSequence of events
- Thread lists
- Conversation screen
- Citations
- Failure + retry UX
- Ask about this document

## iE7 — Background upload / sync ([#7](https://github.com/EzraGubbay/quire-ios/issues/7))

Background refresh (BGTaskScheduler), offline pinning, and background uploads with a Share Extension.

Planned stories:
- e2e journey first
- Background app refresh sync
- Offline pinning
- Upload queue (background URLSession)
- Share Extension → course picker
- Upload status UI

## iE9 — Release: signing + distribution ([#8](https://github.com/EzraGubbay/quire-ios/issues/8))

A signed build distributed to the user's device.

Planned stories:
- Signing + provisioning (human; Apple Developer account)
- Release build configuration
- Release workflow
- Distribution channel (TestFlight vs ad-hoc — needs decision)
- v1.0.0 acceptance

## Sprints (milestones, all planned / closed)

- iOS Sprint 1 — Scaffold, Shell & Sign-in (v0.1.0) — PLANNED — after Android v1.1.0. iE0 scaffold + CI, iE2 shell, iE3 auth.
- iOS Sprint 2 — Browse & Read (v0.2.0) — PLANNED — after Android v1.1.0. iE4 browser, iE5 viewer + downloads.
- iOS Sprint 3 — AI Chat (v0.3.0) — PLANNED — after Android v1.1.0. iE6 AI chat.
- iOS Sprint 4 — Sync & Release (v1.0.0) — PLANNED — after Android v1.1.0. iE7 background sync/upload, iE9 release.
