<p align="center">
  <img src="https://img.shields.io/badge/GitHub-Action-2088FF?logo=github-actions&logoColor=white" alt="GitHub Action" />
  <img src="https://img.shields.io/badge/License-MIT-green?logo=opensourceinitiative&logoColor=white" alt="MIT License" />
</p>

<h1 align="center">🔄 Purge Camo Cache</h1>

<p align="center">
  <b>Keep your GitHub images fresh!</b><br/>
  A GitHub Action that purges cached images served via <code>camo.githubusercontent.com</code>.
</p>

---

## ❓ Why?

GitHub uses **Camo** as a caching proxy to serve images securely. But Camo doesn't refresh images automatically — so your badges and images can stay stale for hours. This action forces a cache purge so updates show up instantly. ⚡

## 🚀 Quick Start

Add this workflow to your repository:

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
        uses: Angrido/Purge-Camo-Cache@v1.3.0
```

🔒 For **private repositories**, pass a token with read access:

```yaml
      - name: Purge Camo Cache
        uses: Angrido/Purge-Camo-Cache@v1.3.0
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```

## 📥 Inputs

| Name    | Required | Default              | Description                       |
|---------|----------|----------------------|-----------------------------------|
| `token` | No       | `${{ github.token }}` | 🔑 GitHub token for authentication. |

## ⚙️ How It Works

1. 🌿 Detects the current branch using `tj-actions/branch-names`.
2. 🔍 Fetches the repository page and extracts all `camo.githubusercontent.com` image URLs.
3. 🧹 Sends a `PURGE` request to each URL to invalidate the cache.

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/Angrido">Angrido</a>
</p>
