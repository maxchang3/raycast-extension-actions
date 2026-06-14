# Changelog

## [1.5.0](https://github.com/maxchang3/raycast-extension-actions/compare/v1.4.0...v1.5.0) (2026-06-14)


### Features

* update sync branch naming and implement idempotent PR creation with force-push support ([6c9ac1a](https://github.com/maxchang3/raycast-extension-actions/commit/6c9ac1a5435ce41007ff16cc58aec6740f4f9cd2))

## [1.4.0](https://github.com/maxchang3/raycast-extension-actions/compare/v1.3.0...v1.4.0) (2026-06-14)


### Features

* add sync-to-fork action to synchronize local extension changes to a fork branch ([011bc16](https://github.com/maxchang3/raycast-extension-actions/commit/011bc16ef82a0a6ecd16dc09c3079cfc0860887f))

## [1.3.0](https://github.com/maxchang3/raycast-extension-actions/compare/v1.2.0...v1.3.0) (2026-06-10)


### Features

* simplify sync branch management by using a static upstream-sync branch and re-using existing pull requests ([928e8c3](https://github.com/maxchang3/raycast-extension-actions/commit/928e8c36b9d290736e36a3c68edf4078b58a4e03))

## [1.2.0](https://github.com/maxchang3/raycast-extension-actions/compare/v1.1.2...v1.2.0) (2026-06-10)


### Features

* add timestamp check to skip upstream syncs when no new changes exist ([d02d7a7](https://github.com/maxchang3/raycast-extension-actions/commit/d02d7a725b43119b337e518bb7999e9ae41354ac))
* update git commit and PR title ([1beb4e1](https://github.com/maxchang3/raycast-extension-actions/commit/1beb4e1b80f2de512a8f0f136e65b2c8f87e5de6))

## [1.1.2](https://github.com/maxchang3/raycast-extension-actions/compare/v1.1.1...v1.1.2) (2026-06-10)


### Bug Fixes

* use correct fork input variable for fork logic check ([6f6bd44](https://github.com/maxchang3/raycast-extension-actions/commit/6f6bd4468ab1bdd7de764fa523ec345c21c260a4))

## [1.1.1](https://github.com/maxchang3/raycast-extension-actions/compare/v1.1.0...v1.1.1) (2026-06-10)


### Bug Fixes

* **sync:** rename raycast_extensions_fork_repo to raycast_extensions_fork_full_name in action configuration ([e51b63e](https://github.com/maxchang3/raycast-extension-actions/commit/e51b63e1b68f059be9379f237eb319115dc75fea))

## [1.1.0](https://github.com/maxchang3/raycast-extension-actions/compare/v1.0.2...v1.1.0) (2026-06-10)


### Features

* add support for syncing from a fork when an active PR is detected ([1c1ddd3](https://github.com/maxchang3/raycast-extension-actions/commit/1c1ddd36a77a93bbf6ee8061728f6eb49c4e9c17))


### Bug Fixes

* add existence check for extension directory to prevent errors when upstream path is missing ([5dc686f](https://github.com/maxchang3/raycast-extension-actions/commit/5dc686fc62db555793bea3340d1b3cf461315812))

## [1.0.2](https://github.com/maxchang3/raycast-extension-actions/compare/v1.0.1...v1.0.2) (2026-06-10)


### Bug Fixes

* simplify sync logic by removing timestamp checks in favor of git status comparison ([ee96c70](https://github.com/maxchang3/raycast-extension-actions/commit/ee96c7044647c05d8a6cca9f46f0a578fe75151e))

## [1.0.1](https://github.com/maxchang3/raycast-extension-actions/compare/v1.0.0...v1.0.1) (2026-06-10)


### Miscellaneous Chores

* release 1.0.1 ([e89931d](https://github.com/maxchang3/raycast-extension-actions/commit/e89931df1b85f72f0513713cf22fced8e8bea95b))

## 1.0.0 (2026-06-10)


### Miscellaneous Chores

* release 1.0.0 ([07de7dd](https://github.com/maxchang3/raycast-extension-actions/commit/07de7dd00babc7f9f5332de2f2ee7e1e3de36af1))
