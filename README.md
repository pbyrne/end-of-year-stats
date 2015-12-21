# End-of-Year Stats

Generating stats for end-of-year retrospectives.

Setup
-----

This script uses environment variables to configure your authentication. Create `.env` in this directory with the following values:

```
export GITHUB_TOKEN='token'
```

You can generate a new GitHub API token on [in your Personal access tokens page](https://github.com/settings/tokens).

Usage
-----

Generate end-of-year statistics for the given year with:

```
YEAR=2015 ORG=dribbble bundle exec rake github:year
```

Sample output:

```
Generating end-of-year statistics for dribbble in 2014.
Repo: example.com/example
  - PRs: 508
  - Comments: 9710
  - Commits: 1543
Repo: example.com/secret-project
  - PRs: 30
  - Comments: 232
  - Commits: 131
TOTAL:
  - PRs: 538
  - Comments: 9942
  - Commits: 1674
```
