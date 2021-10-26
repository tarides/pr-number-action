# pr-number-action

This GitHub Action will search for a `#<PR_NUMBER>` token in `CHANGES.md` and
write a suggestion in your PR to replace this with the current PR's number.

Note: This only works on `pull_request` and `pull_request_target` events!

## Usage

First, set up the action. See below in the examples how to do so.

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

### Example

Add this to your GitHub workflow:

```yaml
- name: Update PR number
  uses: tarides/pr-number-action@v1
```

### Full example

```yaml
name: Populate GitHub PR number in Changelog
on: [pull_request]
jobs:
  Populate-Changelog-Action:
    runs-on: ubuntu-20.04
    steps:
      - name: Update PR number
        uses: tarides/pr-number-action@v1
```
