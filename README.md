# News Aggregator — Mobile

## Template copy

This repo is one of the name-substituted Jetpack Compose (Android + pure-Kotlin `core`) template copies in
`bookchaowalit-mobile`: same project scaffold, build setup and CI as the
canonical template, with its own domain logic in `core/`. The canonical
Jetpack Compose (Android + pure-Kotlin `core`) template is
[`bookchaowalit-mobile/content-photo-mobile`](https://github.com/bookchaowalit-mobile/content-photo-mobile).
Consolidation or archiving of the copies is pending owner decision D5 (BD-033),
per `repository-catalog/portfolio/MOBILE-CONSOLIDATION-2026-10.md` in
solo-empire. Until then this repo is maintained at L1: fail-closed CI
(`.github/workflows/build.yml`: `./gradlew -p core build` with unit tests, then `./gradlew :app:assembleDebug`) plus the shared `security.yml` scan
(gitleaks, Semgrep, OSV-Scanner, Trivy) from `bookchaowalit/platform-ci-workflows`.

Jetpack Compose Android app for **News Aggregator** — one reading list merged from several news feeds.

Part of [Chaowalit Greepoke](https://bookchaowalit.com)'s 101 Portfolio Projects.

## Status

- `core/` — pure-Kotlin domain logic with unit tests. Builds and tests
  without the Android SDK. **This is the verified part of the repo.**
- `app/` — Compose UI shell (Home / Explore / Profile tabs). It depends on
  `core`, but the screens do not use it yet, and the Android build has so far
  only been checked in CI, not locally. See [docs/UPGRADE-PLAN.md](docs/UPGRADE-PLAN.md).

## Core features (`core/`, package `com.bookchaowalit.newsaggregator`)

- URL canonicalisation for de-duplication (host case, `www.`, default ports, fragments, trailing slash, `utm_*`/`fbclid`/`gclid` removed, params sorted)
- Feed merge that drops duplicate URLs and same-title stories across sources, keeping the earliest copy; newest first
- Filtering by source, keyword, muted keywords and a `since` cut-off
- Grouping by local calendar day (time-zone aware)
- Relative time labels (`5m ago`, `3h ago`, `2d ago`, ISO date after a week); uses `java.time` (min SDK 26)

## Tech Stack

- **UI:** Jetpack Compose + Material 3 (Compose BOM 2024.06)
- **Language:** Kotlin 2.0 (Compose compiler Gradle plugin)
- **Android:** AGP 8.5, min SDK 26, target SDK 34
- **Build:** Gradle 8.10 wrapper (committed); `core` is an included build

## Getting Started

Requires JDK 17+.

```bash
./gradlew -p core build          # domain logic + unit tests, no Android SDK needed
./gradlew :app:assembleDebug     # needs the Android SDK (ANDROID_HOME or local.properties)
```

CI (`.github/workflows/build.yml`) runs both; either failing fails the workflow.

## Related

- **Frontend:** [bookchaowalit-website/news-aggregator-frontend](https://github.com/bookchaowalit-website/bookchaowalit-news-aggregator-frontend)
- **Portfolio:** [bookchaowalit.com](https://bookchaowalit.com)

## License

MIT
