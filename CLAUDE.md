# Mascot ordering prototype — instructions for Claude

## What this is
A food-ordering app prototype for [BRAND NAME]. The mascot reacts to ordering events
so the app doesn't feel generic. Ordering speed always comes first: the mascot never
blocks, covers or delays checkout.

## Folder layout
- `design/mascot.svg` — source artwork. Never edit it; changes happen in the design tool.
- `rive/mascot.riv` — exported Rive file that the app loads.
- `app/` — the ordering prototype (Flutter). The `.riv` is copied into `app/assets/`
  and listed in `pubspec.yaml`.
- `docs/` — notes, screenshots, decisions.

## Tools
- The `rive` MCP server controls the open Rive desktop editor. The editor must be open
  with the mascot file and the `Mascot` artboard before you start. If the server isn't
  connected, stop and tell me instead of guessing.
- Skill in `.claude/skills/`: `rive-animations` (animation principles for the moods).
  Use it for technique, but if it conflicts with this file, this file wins. In
  particular, use view model data binding, not state machine inputs. Its code samples
  are React; ignore them, the app is Flutter.
- Before any large edit, ask me to save or duplicate the Rive file first.
- Commit app code to git after each stage I approve.

## Art rules
- The imported SVG is the character. Animate it; don't redraw, recolor or reshape it.
- Ask before adding new shapes (hidden helper groups for pivots are fine).
- Set each part's origin/pivot before keyframing: arms at the shoulder, head at the neck,
  body at its base, eyes at their centre.
- If a part needed for an animation is missing or merged with another (for example both
  eyes in one path), stop and tell me so I can fix the SVG.

## Rive file contract
The app depends on these exact names. Don't rename them.

- Artboard: `Mascot`
- State machine: `MascotSM`
- View model: `MascotVM`, bound to the artboard, with:
  - `mood` (enum): `idle`, `hungry`, `happy`, `cooking`, `celebrate`, `sorry`
  - `itemAdded` (trigger): quick hop or nod, then back to the current mood
  - `cartCount` (number, optional): only if a visual like a filling plate makes sense

| mood      | app moment                     | animation                                    |
|-----------|--------------------------------|----------------------------------------------|
| idle      | browsing the menu              | breathing loop                               |
| hungry    | cart is empty                  | glances at the menu, licks lips, loops       |
| happy     | cart has items                 | gentle bounce loop                           |
| cooking   | order being prepared           | stirring or flipping loop                    |
| celebrate | order confirmed or delivered   | one-shot jump, then returns to happy         |
| sorry     | error or item out of stock     | one-shot droop, then returns to idle         |

Blinking runs on its own state machine layer (every 3–5 s) so it plays over every mood.

## Animation rules
- Loops: 2–4 s and seamless. One-shots: under 1.2 s.
- Use eased motion; linear only for continuous motion like stirring.
- Blend transitions between moods over 150–250 ms.
- Keep the file small: vectors only, no raster images.

## App integration
- Use the official `rive` package from pub.dev (latest version). Load the file with
  `Factory.rive`, show it with `RiveWidget` and a `RiveWidgetController` selecting the
  `Mascot` artboard and `MascotSM` state machine, and bind with
  `controller.dataBind(DataBind.byName('MascotVM'))`. Set `mood` and fire `itemAdded`
  on that view model instance; never play animations directly.
- The Flutter runtime API changed in recent versions and older tutorials use the
  legacy API. Before writing integration code, read the current docs and follow them
  over anything you remember:
  - https://rive.app/docs/runtimes/flutter/flutter
  - https://rive.app/docs/runtimes/flutter/data-binding
  - https://github.com/rive-app/rive-flutter/blob/master/example/lib/examples/databinding.dart
- Dispose the file, controller and view model instance when the widget is disposed.
- Event mapping:
  - cart empty → `mood = hungry`
  - item added → fire `itemAdded`, then `mood = happy`
  - order placed → `mood = celebrate`, then `mood = cooking`
  - order delivered → `mood = celebrate`
  - error or out of stock → `mood = sorry`
- Respect the system reduce-motion setting (`MediaQuery.disableAnimationsOf(context)`):
  stay in idle with blinking only.
- The mascot never sits on top of buttons, prices or the checkout bar.

## How we work
Work in stages and stop for my review after each one:
1. Inspect the imported artwork. Report the layer structure and anything that will
   block animation (merged parts, unnamed groups, unsupported SVG features).
2. Set pivots, then build idle and blink.
3. Build the remaining moods.
4. Build `MascotVM` and wire `MascotSM` to it.
5. Integrate into the app in `app/`.
