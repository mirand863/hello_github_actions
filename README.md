# Hello Github Actions
This repository shows a basic example on how to use github actions for automatic version bumping and testing

## First step
Create a file called `.github/workflows/bump-version.yml` with the following content:

```yml
# This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the "main" branch
  push:
    branches: [ "main" ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "bump"
  bump:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v3
        with:
          fetch-depth: '0'

      # Tag a new version
      # Default: patch bump
      # Add #minor to pull request message for a minor bump
      # Add #major to pull request message for a major bump
      - name: Bump version and push tag
        uses: anothrNick/github-tag-action@1.36.0
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          WITH_V: true
          DEFAULT_BUMP: patch
```
