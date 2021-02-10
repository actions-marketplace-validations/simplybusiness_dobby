# Dobby

“Dobby is free.”

A Github action which provides chat-ops functionality. You can comment on Pull request to perform various operations.
Currently it supports bumping version for a gem.

## Bump version

### Installation

Add a file to your github workflow `.github/workflows/dobby-action.yml` with following content:

```yaml

name: "dobby action"
on:
  issue_comment:
    types: [created]
jobs:
  pr_commented:
    runs-on: ubuntu-20.04
    if: startsWith(github.event.comment.body, '/dobby')
    
    steps:
      - name: 'bump version' 
        uses: simplybusiness/dobby@v1.0.0
        env:
          ACCESS_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # Change to the file path where you keep the Gem's version.
          # It is usually `lib/<gem name>/version.rb` or in the gemspec file.
          VERSION_FILE_PATH: <VERSION FILE PATH>
```

**NOTE:** Workflow will only work once it merged to default (usually master) branch. It is because event `issue_comment` only work on default branch. See [discussion](https://github.community/t/on-issue-comment-events-are-not-triggering-workflows/16784/4) for more detail.


### How to use

1. Add the following comment in the pull request to bump the version.

```
/dobby version <semver level>
```
where semver level can be minor/major/patch.

2. You can see bot will add a comment on Pull request.
   
   ![Version update comment](docs/images/version-update.png)

