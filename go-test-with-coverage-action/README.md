<img align=right width="168" src="docs/gouef_logo.png">

# Go test with coverage
Go test with coverage Github action

[![GitHub stars](https://img.shields.io/github/stars/gouef/go-test-with-coverage-action?style=social)](https://github.com/gouef/go-test-with-coverage-action/stargazers)
![Usages](https://img.shields.io/endpoint?url=https://github-repo-usages.vercel.app/api/getAction.go?repository=gouef/go-test-with-coverage-action)

## Versions
![Stable Version](https://img.shields.io/github/v/release/gouef/go-test-with-coverage-action?label=Stable&labelColor=green)
![GitHub Release](https://img.shields.io/github/v/release/gouef/go-test-with-coverage-action?label=RC&include_prereleases&filter=*rc*&logoSize=diago)
![GitHub Release](https://img.shields.io/github/v/release/gouef/go-test-with-coverage-action?label=Beta&include_prereleases&filter=*beta*&logoSize=diago)

## Introduction

Run go test and send report to codecov

## Example

```yaml
name: Run tests and upload coverage

on:
  workflow_dispatch:
  pull_request:
    types: [opened, synchronize, edited]
  push:

permissions:
  id-token: write
  contents: read

jobs:
  test:
    name: Run tests and collect coverage
    runs-on: ubuntu-latest
    steps:
      - name: Run tests and upload to coverage
        uses: gouef/go-test-with-coverage-action@main
        with:
          go-version: 1.23.4
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

## Contributors

<div>
<span>
  <a href="https://github.com/actions-user"><img src="https://raw.githubusercontent.com/gouef/go-test-with-coverage-action/refs/heads/contributors-svg/.github/contributors/actions-user.svg" alt="actions-user" /></a>
</span>
<span>
  <a href="https://github.com/JanGalek"><img src="https://raw.githubusercontent.com/gouef/go-test-with-coverage-action/refs/heads/contributors-svg/.github/contributors/JanGalek.svg" alt="JanGalek" /></a>
</span>
</div>

