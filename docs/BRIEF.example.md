# Project brief — example

> This is an example. For a new project, copy it to `docs/BRIEF.md` and fill it in,
> or let Claude interview you and write it. Claude only treats `docs/BRIEF.md` as the
> real brief.

## Project
- **Brand:** [BRAND NAME], a new food franchise
- **What we're building:** a food-ordering app prototype with a reactive mascot
- **Platform:** Flutter
- **Goal:** make ordering feel friendly without slowing it down; speed comes first

## Character
- **Artwork:** `design/mascot.svg`
- **Personality:** cheerful, a little greedy for food, never annoying
- **Where it appears:** menu header, empty cart, order confirmation, order tracking

## Rive names
- Artboard: `Mascot`
- State machine: `MascotSM`
- View model: `MascotVM`
  - `mood` (enum): `idle`, `hungry`, `happy`, `cooking`, `celebrate`, `sorry`
  - `itemAdded` (trigger): quick hop or nod, then back to the current mood
  - `cartCount` (number, optional): only if a visual like a filling plate makes sense

## States
| mood      | app moment                   | animation                                |
|-----------|------------------------------|------------------------------------------|
| idle      | browsing the menu            | breathing loop                           |
| hungry    | cart is empty                | glances at the menu, licks lips, loops   |
| happy     | cart has items               | gentle bounce loop                       |
| cooking   | order being prepared         | stirring or flipping loop                |
| celebrate | order confirmed or delivered | one-shot jump, then returns to happy     |
| sorry     | error or item out of stock   | one-shot droop, then returns to idle     |

Ambient layer: blink every 3–5 s over every mood.

## Event mapping
- cart empty → `mood = hungry`
- item added → fire `itemAdded`, then `mood = happy`
- order placed → `mood = celebrate`, then `mood = cooking`
- order delivered → `mood = celebrate`
- error or out of stock → `mood = sorry`

## Constraints
- Never cover the checkout bar, prices or buttons.
- Reduce motion on: stay idle with blinking only.

## Open questions
- Does the brand already have colors or a logo the mascot must match?
