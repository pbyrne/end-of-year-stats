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
