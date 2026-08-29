# renovate-config

Shared [Renovate](https://docs.renovatebot.com) presets for `brzzdev` repos, so a policy change is one
commit here rather than one PR per repo.

Public because a preset in a private repo only resolves where the Renovate app is also installed on that
repo. There is nothing secret in a preset.

## Presets

| Preset | Extend with | For |
| --- | --- | --- |
| `default.json` | `github>brzzdev/renovate-config` | Everything. `config:recommended`, Dependency Dashboard off. |
| `swift.json` | `github>brzzdev/renovate-config:swift` | Swift apps and packages. Adds the Point-Free grouping. |

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
