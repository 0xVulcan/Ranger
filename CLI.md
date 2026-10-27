# Ranger command-line guide

`ranger-cli` is the command-line tool inside Ranger.app. It asks Ranger's background helper for
data, so most commands need no `sudo`.

## Setup

Add a short alias once:

```bash
echo 'alias ranger=/Applications/Ranger.app/Contents/MacOS/ranger-cli' >> ~/.zshrc && source ~/.zshrc
```

## Everyday commands

| Command | What it shows |
| --- | --- |
| `ranger log` | What agents did in the last hour, grouped into readable lines |
| `ranger net` | Connections agents made |
| `ranger perms` | Privacy permissions (Full Disk Access, Accessibility…) each agent holds |
| `ranger sessions` | Each agent run, with start, end and event count |
| `ranger agents` | The agents Ranger knows, with their ids |
| `ranger helper status` | Whether the background helper is running and collecting |
| `ranger helper restart` | Restarts the helper, no `sudo` needed |
| `ranger doctor` | Checks that the Mac can run Ranger; useful for bug reports |

## Useful options

These work on `log`, `net`, `sessions` and `export`:

| Option | What it does |
| --- | --- |
| `--since` | How far back to look: `30s`, `15m`, `2h`, `3d`, `1w` or a date. Default `1h`. |
| `--agent` | Only one agent, by id from `ranger agents`, such as `claude-code` or `cursor`. |
| `--session` | Only one agent run, by id from `ranger sessions`. |
| `--json` | Machine-readable output. |
| `--raw` | `log` only: one line per event instead of grouped lines. |

## Examples

What Claude Code did in the last two hours:

```bash
ranger log --agent claude-code --since 2h
```

Connections agents have open right now:

```bash
ranger net --now
```

Every app's permissions, not just agents, including denied ones:

```bash
ranger perms --all --denied
```

A day of raw events as JSON Lines, for scripts or analysis:

```bash
ranger export --since 1d > ranger-today.jsonl
```

## Advanced

- **`ranger watch`** streams events live, straight from macOS's event logger. It needs `sudo` and a
  terminal with Full Disk Access. The background helper already does this, so you rarely need it.
- **`ranger replay <file>`** runs a saved event capture through the same pipeline, for testing.
- **`ranger helper install` / `uninstall`** register or remove the background helper. The app's
  onboarding and Settings › Background helper do the same.

Every command accepts `--help`, for example `ranger log --help`.
