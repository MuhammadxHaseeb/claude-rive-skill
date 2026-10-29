# Rive project — instructions for Claude

These rules apply to every project made from this template: characters, games, UI
components, motion pieces or anything else Rive can do. Everything specific to the
current project lives in `docs/BRIEF.md`. Where the project stands lives in
`docs/PROGRESS.md`.

## How this template works
You build the project as working Rive content in code with the Rive CLI: artboards,
view models, state machines, animations and scripts, plus the delivery the brief asks
for (an app, a web page or a `.riv` file). If the brief plans an art pass, you build
with swappable placeholders, push to my Rive account, and a person adds the real art in
the Rive Editor before you finish.

How a particular kind of project is planned, built and tested is in `playbooks/`. The
brief names the kind; read that playbook and follow it alongside this file.

## Start here (every session)
1. Read `docs/BRIEF.md`. If it doesn't exist, interview me to write it:
   - First ask what we're making and pick the kind (`character`, `game`, `ui`,
     `motion`, or `other`). Read `playbooks/<kind>.md` and ask its questions.
   - Use `docs/BRIEF.template.md` as the format; `examples/briefs/` has a filled-in
     brief for each kind. Ask a few questions at a time and propose sensible defaults.
   - Write `docs/BRIEF.md` and stop for my approval. Don't create the Rive project or
     the app until I approve it.
2. Read the playbook for the brief's kind. For `other`, or a project that mixes kinds,
   read the closest playbooks and write the approach (skeleton, milestones, how you'll
   test) into the brief's Plan section for my approval.
3. Read `docs/PROGRESS.md` if it exists and continue from where it says. If I ask
   "where are we?", answer from it.
4. If the brief, a playbook and this file disagree, ask me. The brief decides names and
   behaviour; this file decides how the work is done; a playbook adds to this file for
   its kind.
5. If the brief asks for something Rive isn't suited for (3D, long video, heavy raster
   effects), say so while we write the brief and suggest an alternative.

## Folder layout
- `docs/BRIEF.md` — the project brief (source of truth for names and behaviour).
- `docs/PROGRESS.md` — you keep this up to date: kind, current stage, Rive CLI version,
  milestones done / next / left, art-pass status, feedback to carry forward, open
  decisions. Keep it short.
- `docs/ART_PASS.md` — handoff notes for the artist, only if there is an art pass.
- `docs/screenshots/` — frames you capture for review.
- `design/` — reference art, sketches or mockups, if any. Read them for proportions,
  layout and part names; never edit them.
- `rive/<file>/` — the Rive CLI project (`rive.yaml`, `scene.rml`, scripts, its own
  `AGENTS.md`). `<file>` is the Rive file name in the brief. Builds go to
  `rive/<file>/build/<file>.riv`.
- `app/` — the app, if the brief delivers into one.
- `playbooks/` — how to approach each kind of project. Template material; don't put
  project details here.
- `examples/briefs/` — example briefs for each kind.

## Rive CLI
- Check the setup with `rive doctor` and `rive whoami`. If I'm not logged in (exit
  code 3), ask me to run `rive login` myself; it needs a browser. If the CLI is too old
  (exit code 8), ask me to run `rive update`. Exit code 7 means Rive's service was
  unreachable; retry once, then tell me.
- `rive create` writes an `AGENTS.md` for the installed CLI version into the project.
  Read it before writing any RML or scripts and follow it for syntax, lookups and
  self-checks. For process, names and art rules, this file and the playbook win.
- The CLI changes often. Look things up with `rive docs --search`, `rive schema` and
  `rive docs gotchas` instead of relying on memory or older examples.
- Never start the preview window (`rive rive/<file>`) yourself; it keeps running. Ask
  me to run it in a separate terminal so I can watch your edits live. Use commands that
  finish: `--verify`, `--once`, `--screenshot`, `--test`, `rive inspect`.
- Check your own work before showing me anything: the project passes `--verify`,
  `rive inspect --summary` shows the names in the brief, script tests pass (`--test`),
  and your screenshots look right.
- Test it the way it will be used: set view model properties with `--data`, simulate
  input with `--pointer`, `--key` or `--touch`, step time with `--advance`, and capture
  frames with `--screenshot` into `docs/screenshots/`. The playbook says what to test.

## Pushing and pulling (protect the art)
- `rive push` replaces the linked Rive file's content, including anything drawn in the
  Editor. `rive pull` replaces the local project with the Rive file. Nothing is merged.
- Never push or pull without my OK in chat for that push or pull. Pass `--yes` only
  after I've confirmed.
- Commit to git before every pull, so the change can be reviewed and reverted.
- Once an art pass has started (PROGRESS.md says so), pull before you change anything
  in `rive/`, and never push without pulling first.
- The link to the Rive file is saved in `rive/<file>/rive.yaml` (`push.projectId`,
  `push.fileId`). Commit it.

## Swappable placeholders (when the brief plans an art pass)
- Everything that will get real art is a named group (e.g. `head`, `player`,
  `button_bg`) with the names in the brief. Inside each group, the placeholder is a
  simple shape named `<group>_ph`.
- Animate the groups (position, rotation, scale, opacity), never the placeholder
  shapes, and have scripts move groups rather than draw final art. The artist deletes
  the `_ph` shapes and puts the real art in their place, so the motion must live on the
  groups.
- A group's origin is its pivot: place the group at the point it moves around and
  offset the placeholder inside it.
- Match the reference: if `design/` has artwork, size and place each placeholder to
  match it (measure with a short script if needed), so motion amounts fit the real art.
  With no reference, propose proportions and get my OK on a screenshot.
- A part whose shape changes (a smile and a frown, an icon's two states) gets one
  sibling group per variant, switched by group opacity. Never animate path points.
- Placeholders are flat shapes in clearly different colours, so motion is easy to read.
  Anything that needs bones, meshes or path animation goes on the brief's art-pass list.
- Ask before adding groups that aren't in the brief (hidden helper groups are fine).

If there is no art pass, build the final shapes in code, still as named groups.

## Naming contract
- Use the artboard, state machine, view model, property, script and group names in the
  brief exactly. The app and the art pass depend on them; never rename them on your own.
- Drive behaviour through view models: enums for modes and states, triggers for
  one-shot events, numbers, booleans and strings for data. Use view model data binding,
  not state machine inputs.
- Behaviour that should run over every state (blinking, idle shimmer) goes on its own
  state machine layer.
- Set `main` in `rive.yaml` to the brief's main artboard.

## Quality defaults
- Eased motion; linear only for continuous motion like spinning or scrolling.
- Vectors only and a small file, unless the brief says otherwise.
- The `rive-animations` skill in `.claude/skills/` covers animation technique. Use it,
  but this file and the playbook win where they differ.
- The playbook sets timing and other rules for its kind.

## Delivery
The brief's Delivery section says which of these applies.
- **App.** Use the official Rive runtime for the platform in the brief, and drive the
  content only through its view models; never play animations directly. Runtime APIs
  change and older tutorials use legacy APIs, so before writing integration code, read
  the current Rive docs for that platform (https://rive.app/docs/runtimes) and follow
  them over anything you remember.
  - Flutter: use the latest `rive` package from pub.dev. Load with `Factory.rive`, show
    it with `RiveWidget` and a `RiveWidgetController` selecting the brief's artboard
    and state machine, and bind with
    `controller.dataBind(DataBind.byName('<ViewModel>'))`. Read first:
    - https://rive.app/docs/runtimes/flutter/flutter
    - https://rive.app/docs/runtimes/flutter/data-binding
    - https://github.com/rive-app/rive-flutter/blob/master/example/lib/examples/databinding.dart
  - Copy `rive/<file>/build/<file>.riv` into the app's assets (Flutter:
    `app/assets/<file>.riv`, listed in `pubspec.yaml`) and copy it again whenever the
    Rive project changes.
  - Dispose the file, controller and view model instance when the widget is disposed.
  - Respect the system reduce-motion setting (in Flutter,
    `MediaQuery.disableAnimationsOf(context)`) as the brief describes.
- **Web page.** `--publish=web` publishes a page Rive hosts. It needs `rive login` and
  my OK, since it makes the content public.
- **`.riv` file.** Hand over the built file and a short note listing the artboard,
  state machine and view model names and how to drive them.
- Files with scripts must be signed with `--publish` to run on the web. A signed file
  may be watermarked unless the Rive file is in a Cadet-or-higher workspace.

## How we work
Work in stages and stop for my review after each one. After each stage I approve,
create or update `docs/PROGRESS.md` and commit.

1. **Brief.** Interview me (or read my draft) and write `docs/BRIEF.md`. Stop for my
   approval.
2. **Setup and skeleton.** Check the CLI (see above). Create the project with
   `rive create rive/<file>` (or run `rive create <file>` from inside `rive/` if the
   CLI won't take a nested path) and read its `AGENTS.md`. Fill in the brief's Plan
   section from the playbook (groups, milestones, how you'll test) for my OK. Then
   build the skeleton the playbook describes: artboards, named groups or placeholders,
   view models, state machines and script stubs, with no behaviour yet. Verify, inspect
   and show me a screenshot. From here the names are fixed, so app work can run in
   parallel.
3. **Milestones, one at a time**, in the order of the Plan. Each time I say "Do stage
   3", build only the next one:
   a. Describe the plan: what changes, how it moves or behaves, timing, and how you'll
      test it. Wait for my OK before building.
   b. Build it, verify, run tests, and capture frames by driving it the way it will be
      used.
   c. Show me the frames and tell me what to check in the preview. Apply my feedback
      before starting the next one, and add lasting feedback to PROGRESS.md so later
      milestones follow it.
   Each time, say which milestone you just built, which is next, and how many are left.
   Stage 3 is done only when every milestone in the Plan is approved.
4. **Delivery.** Build the `.riv` with `--once` and deliver it the way the brief says
   (see Delivery). If the brief delivers into an app and `app/` has no project yet, ask,
   then create it (Flutter: `flutter create app`).
5. **Art pass (only if the brief plans one).** With my OK, push to my Rive account:
   list projects with `rive ls`, ask me which project (and folder) to use, then push
   with `--project` (and `--folder`) and a `--name` label such as `prototype`. Write
   `docs/ART_PASS.md` for the artist: the link to the file (`rive open <fileId>
   --print`), the groups and pivots, "replace only the `_ph` shapes; don't move, rename
   or delete groups", the brief's art-pass list, and "tell Claude when you're done".
   Mark the art pass as started in PROGRESS.md and stop. Without an art pass, skip to
   stage 6.
6. **Finish.** If there was an art pass: commit, pull with my OK, check with
   `rive inspect` that every name in the brief is unchanged, capture each state again,
   and report anything that broke (moved groups, renamed parts, motion that no longer
   fits the art). After fixes, build the final file (`--publish=local` for a signed
   `.riv`; see Delivery), deliver it again and rerun the checks.

## Improving this template
When a project teaches something reusable (a Rive or CLI gotcha, a better rule), tell
me and suggest the line to add here or to the playbook for its kind. When a new kind of
project comes up, suggest a new playbook. Keep project details out of these files.
