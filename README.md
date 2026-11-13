# renovate-config

The shared [Renovate](https://docs.renovatebot.com/) preset for our public repositories.

## Use it

Put this `renovate.json` at the root of a repository:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>zonhoren/renovate-config"]
}
```

`github>zonhoren/renovate-config` loads [`default.json`](default.json) from this repository's `main` branch. The preset is public, so a repository in any GitHub organisation can extend it. The Renovate app still has to be installed on that repository's organisation.

Add a rule to a repository's own `renovate.json` only when that rule is unique to the repository: an ignored path, a package held below a major version, a custom manager for a file Renovate cannot read. Give every such rule a `description` that says why.

## What the preset does

| Setting | Effect |
|---|---|
| `config:best-practices` | Renovate's recommended base, plus pinned digests for GitHub Actions and container images |
| Schedule | PRs are opened or updated before 6 am on Mondays, America/Toronto time |
| `minimumReleaseAge: 5 days` | A release is proposed only once it is five days old, so a compromised or yanked release is usually caught first |
| Grouping | One PR for all patch updates, one for all minor updates, one for GitHub Actions; every major update gets its own PR, labelled `dependency/major` |
| Lock file maintenance | A weekly PR refreshes lock files, so transitive dependencies stay current |
| Limits | At most 2 new PRs an hour and 10 open at once |
| Vulnerability PRs | Off. Dependabot security updates open security fixes, so each fix gets one PR |
| Automerge | Off |

## Change it

Change the policy by changing `default.json`. A change reaches every repository at its next Renovate run, so keep each change to one policy and validate it first:

```sh
npm run validate
```

The `validate` workflow runs the same check on every push and pull request. An invalid preset stops Renovate in every repository that extends it.

This repository keeps policy only: never add credentials, tokens or internal hostnames.

## Licence

[MIT](LICENSE)
