# 🚀 Purge Camo Cache

## 🌟 Overview

Purge Camo Cache is a GitHub Action that purges all cached images served via camo.githubusercontent.com for a given branch of your repository. This ensures that outdated images are refreshed and properly displayed. 🔄

## ❓ Why Use This Action?

GitHub uses Camo, a caching proxy, to serve images securely. However, Camo does not refresh images automatically. This action helps clear the cached images so that updates are reflected immediately. ⚡

## 🛠️ Usage

To use this GitHub Action, add the following workflow to your repository:

```yaml
name: Purge Camo Cache

on:
  push:
    branches:
      - main
  schedule:
    - cron: '0 */2 * * *'

jobs:
  purge-badges-cache:
    runs-on: ubuntu-latest
    
    steps:
      - name: Purge badges cache
        uses: Angrido/Purge-Camo-Cache@v1.1.0
        with:
          repository: 'Angrido/Angrido' #Change me
          branch: 'main' #Change me if different
```

## 🔍 How It Works

1. 🔄 Detects the current branch using `tj-actions/branch-names`.
2. 🖼️ Extracts all cached image URLs from `camo.githubusercontent.com`.
3. 🚀 Sends a `PURGE` request to refresh those images.
