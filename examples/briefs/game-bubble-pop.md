# Project brief — Bubble Pop

## Project
- **Kind:** game
- **What we're building:** a one-screen arcade game. Bubbles rise from the bottom; tap
  them before they reach the top.
- **Goal:** a quick, satisfying game people play for 1–2 minutes and want to replay
- **Audience:** casual players on phones and desktop browsers
- **Status:** prototype

## Look and feel
- **Reference art:** none
- **Style:** soft, bright, bouncy; satisfying pops
- **Colours and fonts:** pastel bubbles on a deep blue background; one rounded font
- **Art plan:** code-built art is final

## Rive names
- Rive file: `bubble_pop` (CLI project in `rive/bubble_pop/`)
- Artboard: `Game` (390 × 844, portrait)
- State machine: `GameSM`
- View model: `GameVM`
  - `mode` (enum): `title`, `playing`, `gameOver`
  - `score` (number), `lives` (number, starts at 3), `highScore` (number)
  - `start` (trigger), `restart` (trigger)
- Scripts: `game` (spawning, movement, popping, difficulty), `rules_test` (Test script)

## Behaviour
**Rules**
- A bubble spawns every 0.8 s at a random x and rises at 120 px/s.
- Tapping a bubble pops it: +1 point. Golden bubbles (1 in 15) are worth 5.
- A bubble reaching the top costs a life. At 0 lives the game ends.
- Every 10 points, spawning gets 10% faster and bubbles rise 8% faster.

| screen   | what's on it                         | in / out                          |
|----------|--------------------------------------|-----------------------------------|
| title    | name, high score, "Tap to play"      | start → playing                   |
| playing  | bubbles, score, lives                | lives = 0 → gameOver              |
| gameOver | final score, high score, "Play again"| restart → playing                 |

## Inputs and events
- tap or click on a bubble → pop it, add to `score`
- tap on the title or game-over screen → fire `start` or `restart`

## Delivery
- **Where it goes:** a web page hosted by Rive (`--publish=web`)
- **Details:** portrait layout, centred on desktop

## Constraints
- 60 fps on a mid-range phone with 20 bubbles on screen.
- Every tap shows feedback immediately, even a miss.
- Reduce motion on: no screen shake; pops fade instead of bursting.

## Plan
Claude fills this in during stage 2 (groups, milestones, tests).

## Open questions
- Should the high score persist between visits?
