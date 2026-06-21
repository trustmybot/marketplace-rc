# TMB plugin marketplace — RC

Catalog for the **rc channel** of the [TMB plugin](https://github.com/trustmybot/plugin). Pins the latest `vX.Y.Z-rc.N` tag under validation — the release candidate that's passed the local L6 chain and is being re-confirmed by the CI release-gate before it ships as stable. Use this when you want to dogfood a build that's close to release but ahead of the stable channel.

## Install

```
/plugin marketplace add trustmybot/marketplace-rc
/plugin install tmb@trustmybot-rc
```

The rc channel installs as `tmb` (same name as the released plugin), so only one can be enabled at a time.

### Disable any existing `tmb` install first

```
/plugin disable tmb
```

Use `/plugin disable` rather than `/plugin uninstall` so you can flip back to the released channel with `/plugin enable tmb` when done.

### When CC asks for scope, pick *local*

`/plugin marketplace add` will prompt:

```
  Install for all collaborators on this repository (project scope)
> Install for you, in this repo only (local scope)
```

**Pick local scope.** The rc channel is a per-developer choice; teammates may each be on a different channel (stable / rc / dev). Project scope is right only when a team wants everyone pinned to the same channel.

## Pull the latest rc

The marketplace ref is the current `vX.Y.Z-rc.N` tag, but CC caches a clone — when the channel re-pins to a newer rc tag, refresh to pick it up:

```
/plugin marketplace update trustmybot-rc
/plugin update tmb@trustmybot-rc
```

`/reload-plugins` only re-reads what CC already has on disk; you need `marketplace update` + `update` to fetch the newly-pinned tag from the remote.

## Flip back to the released channel when done

```
/plugin uninstall tmb@trustmybot-rc
/plugin enable tmb
```

## Channel routing

- This catalog: **RC channel** (latest `vX.Y.Z-rc.N` tag — pre-release builds under validation)
- [trustmybot/marketplace-dev](https://github.com/trustmybot/marketplace-dev) — dev channel (`trustmybot/plugin@dev` — bleeding edge)
- [trustmybot/marketplace](https://github.com/trustmybot/marketplace) — production (stable tags from main)

## Source

Plugin code lives at [trustmybot/plugin](https://github.com/trustmybot/plugin). This repo contains only the marketplace catalog (`.claude-plugin/marketplace.json`).
