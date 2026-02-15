# Purge Camo Cache

## Overview

A GitHub Action that purges cached images served via `camo.githubusercontent.com` for your repository. GitHub uses Camo as a caching proxy to serve images securely, but it does not refresh them automatically. This action clears the cache so updated images are displayed immediately.

## Usage

Add the following workflow to your repository:

```yaml
name: Purge Camo Cache

on:
  push:
    branches:
      - main
  schedule:
    - cron: '0 */2 * * *'

jobs:
  purge-camo-cache:
    runs-on: ubuntu-latest

    steps:
      - name: Purge Camo Cache
        uses: Angrido/Purge-Camo-Cache@v1.2.0
```

For private repositories, pass a token with read access:

```yaml
      - name: Purge Camo Cache
        uses: Angrido/Purge-Camo-Cache@v1.2.0
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Name    | Required | Default              | Description                                |
|---------|----------|----------------------|--------------------------------------------|
| `token` | No       | `${{ github.token }}` | GitHub token for authentication.          |

## How It Works

1. Detects the current branch using `tj-actions/branch-names`.
2. Fetches the repository page and extracts all `camo.githubusercontent.com` image URLs.
3. Sends a `PURGE` request to each URL to invalidate the cache.
