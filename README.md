<p align="center">
  <a href="https://github.com/cabcookie/action-pr-changelog-reminder/actions"><img alt="typescript-action status" src="https://github.com/cabcookie/action-pr-changelog-reminder/workflows/build-test/badge.svg"></a>
</p>

# GitHub action to remind you to add a changelog

When added to your `.github/workflows` this action will check for a changelog file at every pull request and will remind you to add one if it is missing. It will fail the checks as well.

## Installation

To configure the action simply add the following lines to your `.github/workflows/rebase.yml`:

```yml
name: PR Changelog Reminder

on:
  push:
    branches:
      - main
    paths-ignore:
      - '**.md'
  pull_request:
    paths-ignore:
      - '**.md'

jobs:
  check-for-changelog:
    name: Check for existing changelog

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@main
      - name: Search changelog
        uses: cabcookie/action-pr-changelog-reminder@v1.0.0
        with:
          changelog_regex: 'changelog\/v(0|[1-9][0-9]*)\.(0|[1-9][0-9]*)\.(0|[1-9][0-9]*)-?[a-z0-0]*\/CHANGELOG.md'
          customPrComment: '@cabcookie A changelog for this pull request is missing. Please add it to `changelog/[version]/CHANGELOG.md`.'
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
