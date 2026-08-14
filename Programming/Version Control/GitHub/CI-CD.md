#github #cicd #github-actions #ci #branch-protection

[GitHub Actions](https://docs.github.com/en/actions) runs checks (lint, tests, build) automatically on events like a pull request, giving a pass/fail signal before code merges.

## Minimal Workflow

`.github/workflows/ci.yml`, triggered on every PR targeting `main`:

``` yaml
name: CI
on:
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: echo "replace with the project's real test/lint command"
```

The job name (`test` here) is what shows up as a status check on the PR.

## Require It to Pass Before Merging

Once a workflow exists, tighten [[Branch Protection]] so its check must pass, `contexts` must match the job name(s) exactly:

``` bash
gh api -X PUT repos/<owner>/<repo>/branches/main/protection \
  -H "Accept: application/vnd.github+json" \
  --input - <<'EOF'
{
  "required_status_checks": {
    "strict": true,
    "contexts": ["test"]
  },
  "enforce_admins": false,
  "required_pull_request_reviews": {
    "required_approving_review_count": 0
  },
  "restrictions": null,
  "allow_force_pushes": false,
  "allow_deletions": false
}
EOF
```

`strict: true` also requires the branch to be up to date with `main` before merging, so the check ran against the latest base, not a stale one.
