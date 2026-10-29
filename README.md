# Claude + Rive mascot starter

A reusable template for building an interactive Rive mascot with Claude Code and
dropping it into an app (Flutter by default). The rules live in `CLAUDE.md`, which
Claude reads automatically; each project's details live in `docs/BRIEF.md`.

## What's inside

```
.
├── CLAUDE.md                      # reusable rules and stages for Claude
├── .mcp.json                      # connects Claude Code to the Rive editor
├── .claude/skills/rive-animations # animation-principles skill (MIT, Dylan Tarre)
├── docs/BRIEF.example.md          # example brief (food-ordering mascot)
├── design/                        # put your artwork here (mascot.svg)
├── rive/                          # exported .riv goes here
└── app/                           # your app
```

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [Rive desktop app](https://rive.app/downloads) (macOS or Windows)
- Flutter SDK (or the SDK for the platform in your brief)
- A Rive Cadet plan or higher, only when you export the final `.riv`

## Start a new project

1. Create a copy of this repo (on GitHub: **Use this template**) and open it in VS Code.
2. Write the brief, either way:
   - Let Claude Code interview you: run `claude` and say `Let's start.`
   - Or copy `docs/BRIEF.example.md` to `docs/BRIEF.md` and fill it in (a chat with
     Claude can draft it for you).
3. Save your artwork in `design/`. Put every moving part in its own named group
   (`head`, `eye_L`, `eye_R`, `arm_L`, ...), outline any text, and export with inline
   styles / presentation attributes.
4. Create the app, for Flutter: `flutter create app`
5. Open the Rive desktop app, create a file with the artboard named in the brief, drag
   in your artwork, save, and keep Rive open.
6. In this folder run `claude`. Approve the `rive` MCP server when asked, then check
   it with `/mcp`.

## Prompts

1. `Do stage 1.`
2. `Do stage 2.` (or give feedback first)
3. `Do stage 3.`
4. `Do stage 4.`
5. Export the `.riv` into `rive/`, then: `Do stage 5.`

Claude stops after each stage so you can review it in Rive.

## Improving the template

When a project teaches you something reusable, add it to `CLAUDE.md` here so the next
project starts with it. Keep project details out of `CLAUDE.md`; they belong in the
brief.

## Credits

`.claude/skills/rive-animations` is from
[dylantarre/animation-principles](https://github.com/dylantarre/animation-principles)
under the MIT license; see its `LICENSE` file.
