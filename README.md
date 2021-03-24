# check-wip

> A GitHub Action sets a PR status to pending when any label or keyword in the title indicating it is WIP.

## Usage

Create a `.github/workflows/wip.yml` file in the repository you want to install this action, then add the following to it:

```yml
name: WIP

on:
  pull_request:
    types:
      - opened
      - synchronize
      - reopened
      - edited
      - labeled
      - unlabeled

jobs:
  WIP:
    runs-on: ubuntu-latest
    steps:
      - uses: bubkoo/check-wip@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

          # Comma separated and case sensitive labels.
          labels: do-not-merge, wip, rfc

          # Comma separated and case insensitive keywords.
          keywords: WIP, RFC

          # A string label to differentiate this status from the status of
          # other systems. This field is case-insensitive.
          # @see: https://docs.github.com/en/rest/reference/repos#create-a-commit-status
          context: WIP

          # The target URL to associate with this status. This URL will be
          # linked from the GitHub UI to allow users to easily see the source
          # of the status. For example, if your continuous integration system
          # is posting build status, you would want to provide the deep link
          # for the build output for this specific SHA: http://ci.example.com/user/repo/build/sha
          # @see: https://docs.github.com/en/rest/reference/repos#create-a-commit-status
          target_url: ''

          # A short description of the status.
          # @see: https://docs.github.com/en/rest/reference/repos#create-a-commit-status
          wip_description: work in progress
          ready_description: ready for review
```

And the shortest configuration looks like this:

```yml
name: WIP
on:
  pull_request:
    types:
      - opened
      - synchronize
      - reopened
      - edited
      - labeled
      - unlabeled
jobs:
  WIP:
    runs-on: ubuntu-latest
    steps:
      - uses: bubkoo/check-wip@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE)
