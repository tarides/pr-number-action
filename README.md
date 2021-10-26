# pr-number-action

This GitHub Action will search for a `#<PR_NUMBER>` token in `CHANGES.md` and
write a suggestion in your PR to replace this with the current PR's number.

Note: This only works on `pull_request` and `pull_request_target` events!

## How it works

Create a new line in your `CHANGES.md`:

```markdown
- A change (#<PR_NUMBER>, @your-github-handle)
```

Commit it on a branch and create a pull request. After the action finishes, you
should see a suggestion comment pop up in your branch to replace `#<PR_NUMBER>`
with the number of the pull request you just opened, e.g. `#42`. You can accept
this suggestion at which point it will be committed on your branch.

To add further changes you need to pull from your branch.

Don't worry of you accidentally force-push over it, the action will just run
again and create a new suggestion for you.

## Set up

First, set up the action. Normally it should be run on pull requests of course,
to get the PR number. Due to the way permissions work on Github Actions this
requires the action to be running in the `pull_request_target` context as it
needs to write to the pull request if the pull request comes from a fork (for
local branches it also works in the `pull_request` context).

As such you need to set it to run `on: [pull_request_target]` which will run
the action with the workflow configuration of your target branch.

### Example

Add this to your GitHub workflow:

```yaml
- name: Update PR number
  uses: tarides/pr-number-action@v1.1
```

### Full example

```yaml
name: Populate GitHub PR number in Changelog
on: [pull_request_target]
jobs:
  Populate-Changelog-Action:
    runs-on: ubuntu-20.04
    steps:
      - name: Update PR number
        uses: tarides/pr-number-action@v1.1
```
