# TMB plugin marketplace — RC

Catalog for the **rc channel** of the [TMB plugin](https://github.com/trustmybot/plugin). It pins the release candidate under validation: the `vX.Y.Z-rc.N` tag that passed the local L6 chain and is being re-confirmed by the CI release-gate before it ships as stable. Use it to dogfood a build that is close to release but ahead of stable.

| Channel | Catalog | Plugin source | Version |
|---|---|---|---|
| dev | [`trustmybot-dev`](https://github.com/trustmybot/marketplace-dev) | `trustmybot/plugin@dev-build` | `X.Y.Z-dev.<n>.gh<PR>` |
| **rc** (this one) | `trustmybot-rc` | a `vX.Y.Z-rc.N` tag | `X.Y.Z-rc.N` |
| stable | [`trustmybot`](https://github.com/trustmybot/marketplace) | `trustmybot/plugin@main` | `X.Y.Z` |

Every channel installs the plugin as `tmb`, so one `tmb` is enabled per project at a time. The pinned tag is `plugins[0].source.ref` in `.claude-plugin/marketplace.json`; each rc cut moves it with a `chore(rc): publish vX.Y.Z-rc.N` commit.

## Install

Pick a scope. TMB keeps its trajectory DB and hooks per project, so install it **into the project**, never at user scope:

| Scope | Written to | Use when |
|---|---|---|
| `local` | `.claude/settings.local.json` (git-ignored) | Your own choice of channel; teammates may be on another one. |
| `project` | `.claude/settings.json` (committed) | The whole team pins the same channel. |

Run from the project root. The slash-command form (`/plugin install tmb@trustmybot-rc`) prompts for the scope instead of taking `--scope`.

```bash
claude plugin marketplace add trustmybot/marketplace-rc --scope local
claude plugin install tmb@trustmybot-rc --scope local
```

Replace both `--scope local` with `--scope project` for a team install.

### Switching from another channel

Disable the `tmb` you have before installing this one, at the scope it was installed in. `disable` keeps it so you can `enable` it again later; `uninstall` removes it.

```bash
claude plugin disable tmb@trustmybot --scope local
```

Then restart Claude Code (`/reload-plugins` does not rebind the MCP server or the hooks).

## Upgrade to the newest rc

Claude Code caches a clone of the pinned tag. When the channel re-pins to a newer rc, refresh from the project root:

```bash
claude plugin marketplace update trustmybot-rc
claude plugin update tmb@trustmybot-rc --scope local
```

Then restart Claude Code.

## Back to the stable channel

```bash
claude plugin uninstall tmb@trustmybot-rc --scope local
claude plugin enable tmb@trustmybot --scope local
```

Restart Claude Code afterwards.

## Source

Plugin code lives at [trustmybot/plugin](https://github.com/trustmybot/plugin). This repo holds only the catalog, `.claude-plugin/marketplace.json`.
