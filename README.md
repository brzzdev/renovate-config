# renovate-config

Shared [Renovate](https://docs.renovatebot.com) presets for `brzzdev` repos, so a policy change is one
commit here rather than one PR per repo.

Public because a preset in a private repo only resolves where the Renovate app is also installed on that
repo. There is nothing secret in a preset.

## Presets

| Preset | Extend with | For |
| --- | --- | --- |
| `default.json` | `github>brzzdev/renovate-config` | Everything. `config:recommended`, Dependency Dashboard off. |
| `rust.json` | `github>brzzdev/renovate-config:rust` | Rust crates. Adds monthly lockfile maintenance, so `Cargo.lock` keeps up with transitive releases. |
| `swift.json` | `github>brzzdev/renovate-config:swift` | Swift apps and packages. Adds the Point-Free grouping. |
| `automerge.json` | `github>brzzdev/renovate-config:automerge` | Repos whose ruleset requires a real CI job. Holds supported updates for three days, then automerges minor and patch, excluding 0.x minors. |

`automerge` is opt-in rather than part of the baseline. It turns on GitHub's auto-merge as soon as Renovate
opens the PR, and GitHub then waits only for required checks, so a failing test job the ruleset doesn't
require won't stop the merge. Extend it only where the repo's ruleset requires a real test job.

Lockfile maintenance is never automerged, even where both presets apply: a refreshed lockfile gets no
release-age check, so it could land a crate published minutes earlier.

The three-day hold applies to every supported update, including majors and 0.x minors that still need
human review. Renovate raises security updates immediately without applying the hold.

A repo that needs nothing else is the whole file:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>brzzdev/renovate-config:swift"]
}
```

Repos with their own rules — automerge policy, ecosystem quirks — extend a preset and keep those local,
where the reason for them is next to the code they protect.

## Changing a preset

It applies to every repo on their next Renovate run, with no PR anywhere. Renovate caches resolved presets
for a short while, so a change is not always instant.
