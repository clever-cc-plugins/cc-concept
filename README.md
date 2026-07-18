<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/clever-cc-plugins/.github/main/assets/logo-dark.svg" />
    <img src="https://raw.githubusercontent.com/clever-cc-plugins/.github/main/assets/logo.svg" width="220" alt="clever [cc] plugins" />
  </picture>
</p>

# cc-concept

A [Claude Code](https://claude.ai/code) plugin providing marketing-strategy skills — positioning, competitive analysis, go-to-market, and campaign concepting. cc-concept produces the strategic frame that `cc-content` skills then execute against.

cc-concept runs standalone — it never requires `cc-content` — but recognises and reuses context an existing `cc-content` project already provides.

## At a glance

| Skill                     | What it does                                                               |
| ------------------------- | -------------------------------------------------------------------------- |
| `/cc-concept-onboarding`  | Collect any strategic context downstream skills need but the project lacks |
| `/cc-concept-positioning` | Generate a positioning document and register it as project context         |

Skills are invoked by bare name (e.g. `/cc-concept-positioning`).

> These two skills are the foundation. Competitive-analysis, go-to-market, and campaign-concept skills follow in future releases.

## Installation

Open Claude Code in any project and run:

```
/plugin marketplace add clever-cc-plugins/marketplace
/plugin install cc-concept@clever-cc-plugins
```

### Keeping it current

Auto-update for third-party marketplaces is off by default. To enable it:

1. Run `/plugin` in Claude Code
2. Go to the **Marketplaces** tab
3. Toggle auto-update for `clever-cc-plugins/marketplace`

Once enabled, Claude Code updates the plugin on startup whenever a new version is available.

### Uninstalling

```
/plugin uninstall cc-concept@clever-cc-plugins
```

To remove the marketplace as well:

```
/plugin marketplace remove clever-cc-plugins
```

## License

[MIT](LICENSE) — Copyright (c) 2026 Michael van Laar

---

<p align="center">
  Part of the <a href="https://github.com/clever-cc-plugins">clever-cc-plugins</a> family · <a href="https://github.com/clever-cc-plugins/marketplace">marketplace</a> · <a href="https://github.com/clever-cc-plugins/cc-config">cc-config</a> · <a href="https://github.com/clever-cc-plugins/cc-content">cc-content</a> · <a href="https://github.com/clever-cc-plugins/cc-handoff">cc-handoff</a> · <a href="https://github.com/clever-cc-plugins/cc-chime">cc-chime</a>
</p>
