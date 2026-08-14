#github #branch-protection #pull-request #feature-branch #git

Branch protection blocks direct pushes, force-pushes, and deletion of a branch (typically `main`), so every change has to go through a reviewable pull request instead.

## Enable Branch Protection

``` bash
gh api -X PUT repos/<owner>/<repo>/branches/main/protection \
  -H "Accept: application/vnd.github+json" \
  --input - <<'EOF'
{
  "required_status_checks": null,
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

- `required_status_checks`: `null` until a CI workflow exists, see [[CI-CD]] for wiring one in once it does.
- `enforce_admins: false`: lets the repo owner bypass protection in an emergency instead of getting locked out, set to `true` for a team that wants no exceptions.
- `required_approving_review_count: 0`: still requires opening a PR to merge, just doesn't require someone else's approval, raise this once there's more than one contributor.
- `allow_force_pushes` / `allow_deletions: false`: `main` can't be force-pushed or deleted.

Verify it's active:

``` bash
gh api repos/<owner>/<repo>/branches/main/protection
```

## Feature Branch and PR Workflow

Once `main` is protected, this is the only path for changes to land:

``` bash
git checkout -b feature/<short-description>
# ...commit work...
git push -u origin feature/<short-description>

gh pr create \
  --title "<title>" \
  --body "<body>" \
  --base main \
  --head feature/<short-description> \
  --assignee @me
```

Merge once it's ready:

``` bash
gh pr merge <number> --merge --delete-branch
```

Rebase and autosquash any `fixup!` commits before merging to keep history clean, see [[Keep A Branch Clean]].
