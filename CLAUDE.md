# Rive mascot project — instructions for Claude

These rules apply to every project made from this template. Everything specific to
the current project (brand, app, character, states, names, events) lives in
`docs/BRIEF.md`.

## Start here
1. Read `docs/BRIEF.md` before doing anything else.
2. If it doesn't exist, interview me to write it. Use `docs/BRIEF.example.md` as the
   format: ask a few questions at a time, propose sensible defaults, then write
   `docs/BRIEF.md` and stop for my approval. Don't touch Rive or the app until I
   approve the brief.
3. If the brief and this file disagree, ask me. The brief decides names and behaviour;
   this file decides how the work is done.

## Folder layout
- `docs/BRIEF.md` — the project brief (source of truth for names and behaviour).
- `design/` — source artwork (usually `mascot.svg`). Never edit it; changes happen in
  the design tool.
- `rive/` — the exported `.riv` that the app loads.
- `app/` — the app that uses the animation.
- `docs/` — notes, screenshots, decisions.

## Tools
- The `rive` MCP server (configured in `.mcp.json`) controls the open Rive desktop
  editor. The editor must be open with the project's Rive file and artboard before you
  start. If the server isn't connected, stop and tell me instead of guessing.
- Skill in `.claude/skills/`: `rive-animations` (animation principles). Use it for
  technique, but if it conflicts with this file, this file wins. In particular, use
  view model data binding, not state machine inputs, and ignore its React code
  samples unless the app is React.
- Before any large edit, ask me to save or duplicate the Rive file first.
- Commit app code to git after each stage I approve.

## Art rules
- The imported artwork is the character. Animate it; don't redraw, recolor or reshape it.
- Ask before adding new shapes (hidden helper groups for pivots are fine).
- Set each part's origin/pivot before keyframing: arms at the shoulder, head at the
  neck, body at its base, eyes at their centre.
- If a part needed for an animation is missing or merged with another (for example both
  eyes in one path), stop and tell me so I can fix the artwork.

## Naming contract
- Use the artboard, state machine, view model and property names in the brief exactly.
  The app depends on them; never rename them on your own.
- Drive behaviour through one view model: an enum for the main state (the "mood"),
  triggers for one-shot reactions, and numbers or booleans only where the brief asks.
- Ambient behaviour that should play over every state (blinking, breathing) goes on
  its own state machine layer.

## Animation rules
- Loops: 2–4 s and seamless. One-shots: under 1.2 s, then return to the state the
  brief says.
- Use eased motion; linear only for continuous motion like stirring or spinning.
- Blend transitions between states over 150–250 ms.
- Keep the file small: vectors only, no raster images unless the brief requires them.

## App integration
- Use the official Rive runtime for the platform named in the brief, and drive the
  animation only through the view model; never play animations directly.
- Runtime APIs change and older tutorials use legacy APIs. Before writing integration
  code, read the current Rive docs for that platform (https://rive.app/docs/runtimes)
  and follow them over anything you remember.
- Flutter (default): use the latest `rive` package from pub.dev. Load with
  `Factory.rive`, show it with `RiveWidget` and a `RiveWidgetController` selecting the
  brief's artboard and state machine, and bind with
  `controller.dataBind(DataBind.byName('<ViewModel>'))`. Copy the `.riv` into
  `app/assets/` and list it in `pubspec.yaml`. Read first:
  - https://rive.app/docs/runtimes/flutter/flutter
  - https://rive.app/docs/runtimes/flutter/data-binding
  - https://github.com/rive-app/rive-flutter/blob/master/example/lib/examples/databinding.dart
- Dispose the file, controller and view model instance when the widget is disposed.
- Respect the system reduce-motion setting (in Flutter,
  `MediaQuery.disableAnimationsOf(context)`): stay in the idle state with only subtle
  ambient motion.
- The mascot never covers buttons, prices, form fields or other key UI, and never
  delays the user's main task.

## How we work
Work in stages and stop for my review after each one:
1. Inspect the imported artwork. Report the layer structure and anything that will
   block animation (merged parts, unnamed groups, unsupported SVG features).
2. Set pivots, then build the idle state and ambient layer (for example blinking).
3. Build the remaining states and one-shot reactions from the brief.
4. Build the view model and wire the state machine to it.
5. Integrate into the app in `app/`, following the brief's event mapping.

## Improving this template
When a project teaches something reusable (a Rive gotcha, a better rule), tell me and
suggest the line to add here, so the next project starts with it.
