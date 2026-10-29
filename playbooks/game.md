# Playbook: game

For small interactive games: arcade, puzzle, endless runners, mini-games inside an app.

## Questions for the brief
- What is the core loop, in one sentence? What makes it fun?
- What are the controls (tap, click, drag, keys, gamepad)?
- How do you win, lose and score? Is there a high score?
- How does it get harder over time?
- Which screens: title, playing, paused, game over?
- Where does it run (web page, inside an app, kiosk) and at what size?
- How long is a typical session?
- Sound? Is the art done by hand later (art pass), or is the code-built art final?

## What goes in the brief
- **Rules:** core loop, controls, scoring, win and lose conditions, difficulty curve.
- **Screens table:** screen, what's on it, how you get in and out.
- **Game state:** the view model properties the game and any host app read or set.

## Skeleton (stage 2)
- One artboard at the target size (or one per screen if the brief needs it).
- A named group for every game object type (`player`, `enemy`, `coin`, `hud`), with
  placeholders if there's an art pass.
- One view model for the game state: an enum for the mode (`title`, `playing`,
  `paused`, `gameOver`), numbers for `score`, `lives` or `time`, triggers for `start`,
  `pause` and `restart`.
- A state machine that switches screens on the mode enum.
- Script stubs for the game logic and a Test script. Look up the script types and how
  scripts read input with `rive docs --search`.

## Milestones (stage 3)
1. Grey-box core loop: the main mechanic works with plain shapes, nothing else.
2. Controls and input feel.
3. Win, lose and restart.
4. Scoring and HUD.
5. Difficulty over time.
6. Feedback and juice: hits, pickups, screen shake, transitions.
7. Sound, if the brief asks for it.
8. Polish and performance.

## Testing
- Put the rules (scoring, collisions, lose conditions, difficulty steps) in Test
  scripts and run them with `--test` after every change.
- Play it with simulated input: `--pointer`, `--key` or `--touch`, plus `--advance`,
  then capture frames. Use `--seed` so runs repeat exactly.
- Check game state with `--data-dump` (score, lives and mode change as expected).
- Measure frame time with `--bench` on the busiest moment of the game.

## Rules
- Find the fun before the art: the grey-box loop must work before anything is
  polished.
- Keep logic in scripts and visuals in named groups, so the art can change without
  touching the rules.
- Movement and timers use elapsed time, not frame counts, so speed is the same at any
  frame rate.
- Every input gets visible feedback within one frame.
- Show the score and state through the view model, so a host app can read them.
- Files with scripts must be signed with `--publish` to run on the web (see Delivery in
  `CLAUDE.md`).
