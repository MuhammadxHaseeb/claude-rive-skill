# Claude + Rive starter

A reusable template for building anything in Rive with Claude Code and the Rive CLI:
characters and mascots, games, interactive UI, logo reveals and other motion pieces.
You write (or talk through) a brief; Claude plans, builds, tests and delivers it,
stopping for your review after every step.

Claude builds everything in code first. If you want hand-made art, it builds with
swappable placeholders, pushes the project to your Rive account, and you add the real
art in the Rive Editor before Claude finishes. The motion is keyed on named groups
rather than on the shapes inside them, so it carries over to the new art.

## How it's organised

```
.
├── CLAUDE.md                       # rules and stages for every project
├── playbooks/                      # how to plan, build and test each kind
│   ├── character.md                #   mascots, avatars, guides
│   ├── game.md                     #   small interactive games
│   ├── ui.md                       #   buttons, loaders, components
│   └── motion.md                   #   logo reveals, hero animations, explainers
├── docs/BRIEF.template.md          # blank brief
├── examples/briefs/                # a filled-in brief for each kind
├── .claude/skills/rive-animations  # animation-principles skill (MIT, Dylan Tarre)
├── design/                         # optional reference art, sketches or mockups
├── rive/                           # Claude creates the Rive CLI project here
└── app/                            # your app, if the project goes into one
```

`CLAUDE.md` holds the rules that never change. Each playbook adds what's specific to
one kind of project: the questions to ask, what to build first, the milestones and how
to test them. Your project's details live in `docs/BRIEF.md`, and its progress in
`docs/PROGRESS.md`, so you can stop at any point and pick up in a new session.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [Rive CLI](https://rive.app/docs/cli/getting-started) on macOS (Apple Silicon),
  Windows or Linux
- A Rive account, for an art pass or a Rive-hosted web page
- The Rive Editor ([web or desktop](https://rive.app/docs/editor)), only for an art pass
- The SDK for your app's platform (Flutter by default), only if the project goes into
  an app
- A Rive Cadet plan or higher, only for a final signed file without a watermark

## Start a new project

1. On GitHub, click **Use this template**, then clone your copy and open it.
2. Install the Rive CLI, then run `rive login` and `rive doctor`.
3. Write the brief, either way:
   - Run `claude` and say `Let's start.` Claude asks what you're making and interviews
     you with the right playbook's questions.
   - Or copy `docs/BRIEF.template.md` to `docs/BRIEF.md` and fill it in, using
     `examples/briefs/` as a guide. Then run `claude` and say `Let's start.`
4. Optional: put reference art, sketches or mockups in `design/`.
5. Once Claude has created the Rive project (stage 2), run `rive rive/<file>` in a
   second terminal to watch the preview update as Claude works.

## Stages

| Say                    | What happens                                                       |
|------------------------|--------------------------------------------------------------------|
| `Let's start.`         | 1. Brief: Claude interviews you, you approve                       |
| `Do stage 2.`          | 2. Rive project, plan and skeleton (names, groups, view models)    |
| `Do stage 3.` (repeat) | 3. One milestone at a time: plan, your OK, build, test, feedback   |
| `Do stage 4.`          | 4. Delivery: into the app, a Rive-hosted web page, or a `.riv` file |
| `Do stage 5.`          | 5. Art pass only: push to Rive and write the art-pass notes        |
| (you, in the Editor)   | Art pass, following `docs/ART_PASS.md`                             |
| `Do stage 6.`          | 6. Finish: pull the art if any, final checks, final file           |

Claude stops after each stage so you can review it. Coming back later? Run `claude` and
ask `Where are we?`

## The art pass

Only if your brief plans one. Open the pushed file in the Rive Editor (the link is in
`docs/ART_PASS.md`). In each group, delete the `_ph` placeholder and put the real art in
its place: draw it, or import your SVG and move each piece into the matching group.
Don't move, rename or delete the groups; the animations live on them. Then tell Claude
the art is done and say `Do stage 6.`

A push replaces the Rive file's content, including your art, so Claude always pulls
your changes before it pushes again. Earlier versions also stay in the Editor's
revision history.

## Maintaining the template

- In this repo's GitHub settings, tick **Template repository** so **Use this template**
  appears.
- When a project teaches you something reusable, add it to `CLAUDE.md` or the
  playbook for that kind. Claude suggests these lines as you go.
- For a new kind of project (data visualisation, interactive story, ...), add a
  `playbooks/<kind>.md` with the same sections as the others, and an example brief.
- Keep project details out of `CLAUDE.md` and `playbooks/`; they belong in the brief.

## Credits

`.claude/skills/rive-animations` is adapted from
[dylantarre/animation-principles](https://github.com/dylantarre/animation-principles)
under the MIT license; see its `LICENSE` file. It has been edited for this template, so
don't re-sync it from upstream.
