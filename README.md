# Ranger

**See what your AI agents actually do on your Mac.**

AI agents like Claude Code, Cursor and ChatGPT increasingly run commands, edit files and act on their own. To do that, people grant them broad permissions such as Full Disk Access, Accessibility and Screen Recording, but have no way to see what the agents actually do with that access.

Ranger is a native macOS app that answers two questions:

1. **What can my AI agents access?** A permissions view showing which AI apps hold sensitive macOS permissions.
2. **What did they actually do?** A plain-English activity history of every command and file change an agent makes, e.g. *"Claude Code ran `git push`"* or *"Cursor modified 12 files in ~/projects/app"*.

## Status

🚧 Work in progress. A working prototype already attributes Claude Code's commands using Apple's `eslogger`. The native app and Endpoint Security system extension are in development, and Ranger will be released as soon as Apple grants the Endpoint Security entitlement.

## How it works

- **Endpoint Security**: Ranger uses Apple's Endpoint Security framework to observe process and file events. It subscribes to NOTIFY events only, so it never blocks or modifies anything.
- **Agent attribution**: Ranger builds a live process tree, identifies known AI apps, and follows everything they launch, including shells, scripts and tools several levels deep. Unrelated activity is ignored.
- **Local only**: all data stays on your Mac. Nothing is uploaded.

## Planned features

- Live activity feed, grouped and filtered by agent
- Permissions overview (Full Disk Access, Accessibility, Screen Recording, Automation)
- Recorded sessions: start/stop a recording and replay everything an agent touched
- Alerts for sensitive actions: reading SSH keys or credentials, creating LaunchAgents, running `sudo`
- Command-line tool and an optional local web dashboard
- Export to JSON / SQLite

## Requirements

- macOS 14 or later
- Full Disk Access and approval of the system extension (Ranger walks you through both)

## Distribution

Ranger will be signed with Developer ID, notarized by Apple, and distributed as a DMG via GitHub Releases and Homebrew. It is not distributed through the Mac App Store, because Endpoint Security clients are not supported there.

## License

To be decided.
