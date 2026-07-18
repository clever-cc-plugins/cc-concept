# cc-concept

Marketing-strategy skills for Claude Code, distributed as a plugin in the
[clever-cc-plugins](https://github.com/clever-cc-plugins) family. cc-concept
produces the strategic frame — positioning, competitive analysis, go-to-market,
campaign concepts — that `cc-content` skills then execute against.

## Install

```
/plugin marketplace add clever-cc-plugins/marketplace
/plugin install cc-concept@clever-cc-plugins
```

## Skills (Slice 1)

| Skill                    | Purpose                                                                    |
| ------------------------ | -------------------------------------------------------------------------- |
| `cc-concept-onboarding`  | Collect any strategic context downstream skills need but the project lacks |
| `cc-concept-positioning` | Generate a positioning document and register it as project context         |

Skills are invoked by bare name (e.g. `/cc-concept-positioning`). cc-concept runs
standalone — it never requires `cc-content` — but recognises and reuses context an
existing `cc-content` project already provides.
