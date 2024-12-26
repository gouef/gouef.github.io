<img align=right width="168" src="docs/gouef_logo.png">

# Release action
Github release action

[![GitHub stars](https://img.shields.io/github/stars/gouef/release-action?style=social)](https://github.com/gouef/release-action/stargazers)
![Usages](https://img.shields.io/endpoint?url=https://github-repo-usages.vercel.app/api/getAction.go?repository=gouef/release-action)


## Versions
![Stable Version](https://img.shields.io/github/v/release/gouef/release-action?label=Stable&labelColor=green)
![GitHub Release](https://img.shields.io/github/v/release/gouef/release-action?label=RC&include_prereleases&filter=*rc*&logoSize=diago)
![GitHub Release](https://img.shields.io/github/v/release/gouef/release-action?label=Beta&include_prereleases&filter=*beta*&logoSize=diago)

## Requires

- Workflow permissions read and write

Allow permissions in your repository **Settings** -> **Actions** -> **General** -> Workflow permissions (section) -> Read and write permissions


### Example
```yaml
name: Create Release

on:
  push:
    tags:
      - 'v*'
  workflow_dispatch:
    inputs:
      tag_name:
        description: 'Tag name for the release'
        required: true
        default: 'v1.0.0'
      release_type:
        description: 'Release type (stable, beta, rc)'
        required: true
        default: 'stable'

jobs:
  call-release:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Create release
        uses: gouef/release-action@main
        with:
          branch: ${{ github.ref_name }}
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Contributors

<div>
<span>
  <a href="https://github.com/JanGalek"><img src="https://raw.githubusercontent.com/gouef/release-action/refs/heads/contributors-svg/.github/contributors/JanGalek.svg" alt="JanGalek" /></a>
</span>
<span>
  <a href="https://github.com/actions-user"><img src="https://raw.githubusercontent.com/gouef/release-action/refs/heads/contributors-svg/.github/contributors/actions-user.svg" alt="actions-user" /></a>
</span>
</div>

