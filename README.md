# Hello Github Actions
This repository shows a basic example on how to use GitHub Actions for automatic version bumping.

## Premise
Since we are limited to 5 minutes for the tutorial, I thought of doing it incrementaly. Hence, today is only a short tutorial on automatic version bumping with the semantic versioning scheme, but more topics on CI/CD can be offered in future tutorials if there is interest.

### Why GitHub?
- GitHub brings more visibility to projects;
- It is possible to mirror a GitHub repository on GitLab to comply with DACS' workflow;
- GitHub Actions are easier to use;
- GitHub Actions is unlimited for public repositories;
- GitHub offers 2000 CI minutes per month for private repositories (GitLab only offers 2000 minutes per year).

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
  # Triggers the workflow on push events but only for the "main" branch
  push:
    branches: [ "main" ]

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
      # Add #minor to pull request or commit message for a minor bump
      # Add #major to pull request or commit message for a major bump
      - name: Bump version and push tag
        uses: anothrNick/github-tag-action@1.36.0
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          WITH_V: true
          DEFAULT_BUMP: patch
```

## Second step
Try to update the README and see the tag being bumped on the tab actions.

## Third step
Try to create a pull request and use the tag #minor or #major (you can also just add the tag to the commit message).

## Next tutorial
Is there any specific topic you would like to see in a future tutorial? For example:
- Automatic versioning on GitLab
- Mirroring a GitHub repository on GitLab
- Automatically linting Python code
- Automatically linting R code
- Automatically testing Python code
- Automatically testing R code
- Automatic deployment to pypi
- Automatic deployment to bioconda
- Something else (can also be topics other people could offer)

I will create a poll on Mattermost.
