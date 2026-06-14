# Raycast Extension Actions

> This repository is a unified fork and improvement of [timrogers/publish-raycast-extension](https://github.com/timrogers/publish-raycast-extension) and [timrogers/pull-raycast-extension-changes](https://github.com/timrogers/pull-raycast-extension-changes).

This repository contains three GitHub Actions to help you manage your Raycast extensions smoothly between your local repository and the official `raycast/extensions` repository.

1. **[Publish Raycast Extension](#1-publish-raycast-extension)**: Publish changes from your local repository to the official repository.
2. **[Pull Raycast Extension Changes](#2-pull-raycast-extension-changes)**: Sync upstream changes from the official repository back to your local repository.
3. **[Sync to Fork (Manual PR Updates)](#3-sync-to-fork-manual-pr-updates)**: Sync your current local branch changes to your `raycast/extensions` fork branch.

With these actions, your extension can live in your own repo, but be automatically synced in both directions with `raycast/extensions`.

---

## 1. Publish Raycast Extension

This action allows you to store a custom extension in your own repo, and automatically publish changes to the central `raycast/extensions` repo.

### Features & Improvements

- **Performance Boost**: Uses Git sparse-checkout and partial clone to drastically reduce clone time.
- **Better PR Creation**: Automatically generates Pull Requests with the official Raycast PR template.
- **Intelligent `CHANGELOG.md` Date Replacement**: Safely replaces the release date in your changelog.
- **Ignored Paths**: Specify custom paths to exclude via `ignore_paths`.

### Usage

1. Fork the `raycast/extensions` repo.
2. Add a Personal Access Token (`repo` and `workflow` scopes) as a secret named `GH_ACCESS_TOKEN`.
3. Create `.github/workflows/release.yml`:

> [!TIP]
> It is highly recommended to configure a GitHub Environment (e.g., `raycast-publish`) with **Required reviewers** in your repository settings. By specifying this environment in your job, the workflow will automatically pause and require your manual approval before actually creating the PR to Raycast.

```yaml
name: Publish to Raycast
on:
  release:
    types: [published]

permissions:
  contents: read

jobs:
  publish:
    runs-on: ubuntu-latest
    # Recommended: require manual approval before publishing
    environment: raycast-publish
    steps:
      - uses: maxchang3/raycast-extension-actions/publish@v1
        with:
          raycast_extensions_fork_full_name: your-username/extensions
          github_username: your-username
          extension_name: your-extension-name
          github_access_token: ${{ secrets.GH_ACCESS_TOKEN }}
          # OPTIONAL: List of paths to ignore
          # ignore_paths: |
          #   .vscode
          #   .github
```

---

## 2. Sync `raycast/extension` Changes

This action automatically creates a PR to your repo whenever any changes are made to your extension "upstream" in the `raycast/extensions` repo.

### Features & Improvements

- **Smart Syncing & Ignored Files**: The `ignore_paths` parameter allows you to seamlessly exclude specific files or folders from the upstream sync, keeping your local version completely untouched (e.g. `CHANGELOG.md`).

### Usage

1. Create a `.github/workflows/pull_upstream_changes.yml` file:

```yaml
name: Pull upstream changes
on:
  schedule:
    - cron: "0 5 * * *"
  workflow_dispatch:

permissions:
  contents: write
  pull-requests: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: maxchang3/raycast-extension-actions/sync@v1
        with:
          extension_name: your-extension-name
          # Optional: List of files/folders you DO NOT want to sync back
          ignore_paths: |
            CHANGELOG.md
          github_access_token: ${{ secrets.GITHUB_TOKEN }}
```

---

## 3. Sync to Fork (Manual PR Updates)

This action allows you to sync your current local branch changes to your `raycast/extensions` fork branch (e.g., `ext/your-extension-name`) without publishing a new release or creating a PR to the upstream `raycast/extensions` repository. 

It is designed for the scenario where you already have an open PR and need to push updates based on PR reviews.

### Features & Improvements

- **Safe Syncing**: Copies your local changes to the fork's PR branch while ignoring specific files (like `CHANGELOG.md`), so your manual changelog edits during the PR are preserved.
- **Review Workflow**: Supports a `create_pr` option to create a Pull Request within your *own* fork (against the `ext/your-extension-name` branch) so you can review the synced changes before merging them.

### Usage

It is highly recommended to trigger this action manually via `workflow_dispatch`.

1. Create a `.github/workflows/sync-to-fork.yml` file:

```yaml
name: Sync to Fork
on:
  workflow_dispatch:

permissions:
  contents: read

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: maxchang3/raycast-extension-actions/sync-to-fork@v1
        with:
          raycast_extensions_fork_full_name: your-username/extensions
          github_username: your-username
          extension_name: your-extension-name
          github_access_token: ${{ secrets.GH_ACCESS_TOKEN }}
          # Optional: ignore files you don't want to sync (default shown)
          # ignore_paths: |
          #   CHANGELOG.md
          #   .github
          # Optional: Create a PR in your fork instead of pushing directly to ext/
          # create_pr: false
```

