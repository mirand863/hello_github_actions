# Hello Github Actions
This repository shows a basic example on how to use github actions for automatic version bumping.

## Premise
Since we are limited to 5 minutes for the tutorial, I thought of doing it incrementaly. Hence, today is only a short tutorial on automatic version bumping with the semantic versioning scheme.

### Why GitHub?
GitHub brings more visibility to projects and, as far as I know, it is unlimited for public repositories. However, it still offers 2000 CI minutes per month for private repositories (in contrast with 2000 minutes per year on GitLab). Furthermore, GitHub Actions are easier to use and you can always mirror you github repository on GitLab to comply with DACS' workflow.

## Semantic versioning
Semantic Versioning is a versioning scheme for using meaningful version numbers (that is why it is called Semantic Versioning). Specifically, the meaning revolves around how API versions compare in terms of backwards-compatibility.

Given a version number `MAJOR.MINOR.PATCH`:
| Version | Meaning |
| -------------- | ------- |
| MAJOR | incompatible API changes |
| MINOR | add functionality (backwards-compatible) |
| PATCH | bug fixes (backwards-compatible) |

Further reading: [semver.org](https://semver.org/) and [cheatsheet](https://devhints.io/semver)

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

## Second step
Try to update the README and see the tag being bumped on the tab actions

## Third step
Try to create a pull request and use the tag #minor or #major

## Next tutorial
Is there any specific topic you would like to see in a future tutorial? For example, mirroring a GitHub repository on GitLab, automatically linting Python or R code, automatically testing Python or R code, automatic deployment to pypi and bioconda, etc.
