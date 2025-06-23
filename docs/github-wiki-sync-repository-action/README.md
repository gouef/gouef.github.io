<img align=right width="168" src="docs/gouef_logo.png">

# Github wiki sync repository action
Create / Generate / Update Github wiki based on your repository documentation

[![GitHub stars](https://img.shields.io/github/stars/gouef/github-wiki-sync-repository-action?style=social)](https://github.com/gouef/github-wiki-sync-repository-action/stargazers)
![Usages](https://img.shields.io/endpoint?url=https://github-repo-usages.vercel.app/api/getAction.go?repository=gouef/github-wiki-sync-repository-action)

## Versions
![Stable Version](https://img.shields.io/github/v/release/gouef/github-wiki-sync-repository-action?label=Stable&labelColor=green)
![GitHub Release](https://img.shields.io/github/v/release/gouef/github-wiki-sync-repository-action?label=RC&include_prereleases&filter=*rc*&logoSize=diago)
![GitHub Release](https://img.shields.io/github/v/release/gouef/github-wiki-sync-repository-action?label=Beta&include_prereleases&filter=*beta*&logoSize=diago)


## Requires

- Workflow permissions read and write (Allow permissions in your repository **Settings** -> **Actions** -> **General** -> Workflow permissions (section) -> Read and write permissions)
- (maybe) inicialized Github wiki

### Example
```yaml
name: Update Github wiki

on:
  push:
    branches:
      - main
      - master

permissions:
  contents: write

jobs:
  update-wiki:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Update wiki
        uses: gouef/github-wiki-sync-repository-action@main
        with:
          dir: "docs/"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```


## Contributors

<div>
<span>
  <a href="https://github.com/actions-user"><img src="https://raw.githubusercontent.com/gouef/github-wiki-sync-repository-action/refs/heads/contributors-svg/.github/contributors/actions-user.svg" alt="actions-user" /></a>
</span>
<span>
  <a href="https://github.com/JanGalek"><img src="https://raw.githubusercontent.com/gouef/github-wiki-sync-repository-action/refs/heads/contributors-svg/.github/contributors/JanGalek.svg" alt="JanGalek" /></a>
</span>
</div>

