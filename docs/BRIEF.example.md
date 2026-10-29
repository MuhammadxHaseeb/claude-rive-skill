# Project brief — Bae mascot

## Project
- **Brand:** Bae, a new food franchise that is growing fast and has no website or app yet
- **What we're building:** a food-ordering app prototype with a reactive mascot, to
  pitch to Bae. It should not feel like a generic ordering app.
- **Platform:** Flutter
- **Goal:** make ordering feel friendly and memorable without slowing it down; speed
  always comes first
- **Status:** unofficial pitch prototype. The mascot is a proposal, so keep it in its
  own layer and easy to swap if Bae has or wants a different character.

## Character
- **Artwork:** `design/mascot.svg` (I provide it)
- **Personality:** cheerful, a little greedy for food, warm, never annoying
- **Where it appears:** menu header (small), empty cart, order confirmation, order
  tracking (largest, since people watch that screen while they wait)

## Rive names
- Rive file: `bae_mascot`
- Artboard: `Mascot`
- State machine: `MascotSM`
- View model: `MascotVM`
  - `mood` (enum): `idle`, `hungry`, `happy`, `cooking`, `celebrate`, `sorry`
  - `itemAdded` (trigger): quick hop or nod, then back to the current mood
  - `cartCount` (number, optional): only if a visual like a filling plate makes sense
- Exported file: `rive/bae_mascot.riv`, copied to `app/assets/bae_mascot.riv`

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

## App prototype scope
- Screens: menu, item details, cart, checkout, order confirmation, order tracking
- Use placeholder menu data and fake order progress; no real payments or backend
- Brand colors and fonts: take from the mascot artwork until Bae's brand kit is known

## Constraints
- Never cover the checkout bar, prices, buttons or form fields.
- The mascot never delays a tap or a screen change.
- Reduce motion on: stay idle with blinking only.
- Vectors only; keep the `.riv` small.

## Open questions
- What food does Bae sell (burgers, fries, desserts, desi)? This shapes the cooking
  animation and placeholder menu.
- Does Bae already have a logo, colors or fonts the app and mascot must match?
- What does the mascot look like and what is its name? (Fill in once the SVG is ready.)