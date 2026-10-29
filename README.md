# Claude + Rive mascot starter

A ready-to-use folder for building an interactive Rive mascot with Claude Code and
dropping it into a Flutter app. Claude reads `CLAUDE.md` automatically, so you only
send short prompts like "Do stage 1."

## What's inside

```
.
├── CLAUDE.md                      # rules, naming contract and stages for Claude
├── .mcp.json                      # connects Claude Code to the Rive editor
├── .claude/skills/rive-animations # animation-principles skill (MIT, Dylan Tarre)
├── design/                        # put mascot.svg here
├── rive/                          # exported mascot.riv goes here
├── app/                           # your Flutter app
└── docs/                          # notes and screenshots
```

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [Rive desktop app](https://rive.app/downloads) (macOS or Windows)
- Flutter SDK
- A Rive Cadet plan or higher, only when you export the final `.riv`

## Setup

1. Clone or download this repo.
2. Open `CLAUDE.md` and replace `[BRAND NAME]`.
3. Save your artwork as `design/mascot.svg`. Put every moving part in its own named
   group (`head`, `eye_L`, `eye_R`, `arm_L`, ...), outline any text, and export with
   inline styles / presentation attributes.
4. Create the Flutter app: `flutter create app`
5. Open the Rive desktop app, create a file with an artboard named `Mascot`, drag in
   `design/mascot.svg`, save, and keep Rive open.
6. In this folder run `claude`. Approve the `rive` MCP server when asked, then check
   it with `/mcp`.

## Prompts

1. `Read CLAUDE.md and do stage 1.`
2. `Do stage 2.` (or give feedback first)
3. `Do stage 3.`
4. `Do stage 4.`
5. Export `mascot.riv` into `rive/`, then: `Do stage 5.`

Claude stops after each stage so you can review it in Rive.

## Credits

`.claude/skills/rive-animations` is from
[dylantarre/animation-principles](https://github.com/dylantarre/animation-principles)
under the MIT license; see its `LICENSE` file.
