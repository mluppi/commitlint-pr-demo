**This repository shows how to use [commitlint](https://commitlint.js.org) in a GitHub Action to check commit-messages of commits in pull-requests.**

**See the [commitlint.yml](.github/workflows/commitlint.yml) for the complete workflow.**

Check in the [*Action* tab](https://github.com/mluppi/commitlint-pr-demo/actions/workflows/commitlint.yml) or the [closed pull requests](https://github.com/mluppi/commitlint-pr-demo/pulls?q=is%3Apr+is%3Aclosed) to see the status (successful/failed) of the actions.

---

The straight-forward solution is to use the `--to` and `--from` arguments of `commitlint` with the SHA-1 values instead of the branch names or relative references. On the one hand, this reliably solves the problem of unknown revisions or paths in the working tree. On the other hand, only commits in scope of the PR will be checked. As a sidenote: GitHub uses the same references (SHA-1) for the ad-hoc merge that is being checked-out.

We need the base-SHA as well as the head-SHA. In a GitHub action those values are available in the pull-request object of the event in the `github`-context.

*The the actual linting can be done with the following command:*
```
npx commitlint --from ${{ github.event.pull_request.base.sha }} --to ${{ github.event.pull_request.head.sha }} --verbose
```
