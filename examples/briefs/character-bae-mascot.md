# Project brief — Bae mascot

## Project
- **Kind:** character
- **What we're building:** a reactive mascot for a food-ordering app prototype, to pitch
  to Bae, a new food franchise that is growing fast and has no website or app yet. The
  app should not feel like a generic ordering app.
- **Goal:** make ordering feel friendly and memorable without slowing it down; speed
  always comes first
- **Audience:** Bae's customers ordering on their phones
- **Status:** unofficial pitch prototype. The mascot is a proposal, so keep it in its
  own layer and easy to swap if Bae has or wants a different character.

## Look and feel
- **Reference art:** `design/mascot.svg` (I provide it)
- **Style:** cheerful, a little greedy for food, warm, never annoying
- **Colours and fonts:** take them from the mascot artwork until Bae's brand kit is known
- **Art plan:** placeholders now, art pass in the Rive Editor later

## Rive names
- Rive file: `bae_mascot` (CLI project in `rive/bae_mascot/`)
- Artboard: `Mascot`
- State machine: `MascotSM`
- View model: `MascotVM`
  - `mood` (enum): `idle`, `hungry`, `happy`, `cooking`, `celebrate`, `sorry`
  - `itemAdded` (trigger): quick hop or nod, then back to the current mood
  - `cartCount` (number, optional): only if a visual like a filling plate makes sense

## Behaviour
| mood      | app moment                   | animation                                |
|-----------|------------------------------|------------------------------------------|
| idle      | browsing the menu            | breathing loop                           |
| hungry    | cart is empty                | glances at the menu, licks lips, loops   |
| happy     | cart has items               | gentle bounce loop                       |
| cooking   | order being prepared         | stirring or flipping loop                |
| celebrate | order confirmed or delivered | one-shot jump, then returns to happy     |
| sorry     | error or item out of stock   | one-shot droop, then returns to idle     |

- One-shot reaction: `itemAdded`, a quick hop or nod, then back to the current mood.
- Ambient layer: blink every 3–5 s over every mood.

## Inputs and events
- cart empty → `mood = hungry`
- item added → fire `itemAdded`, then `mood = happy`
- order placed → `mood = celebrate`, then `mood = cooking`
- order delivered → `mood = celebrate`
- error or out of stock → `mood = sorry`

## Delivery
- **Where it goes:** a Flutter app in `app/`
- **Details:** the mascot appears in the menu header (small), the empty cart, order
  confirmation and order tracking (largest, since people watch that screen while they
  wait). Built file `rive/bae_mascot/build/bae_mascot.riv`, copied to
  `app/assets/bae_mascot.riv`.
- **App prototype scope:** screens for menu, item details, cart, checkout, order
  confirmation and order tracking. Placeholder menu data and fake order progress; no
  real payments or backend.

## Art pass
- **Who:** me, in the Rive Editor (web or desktop), after stage 5
- **Tasks the placeholders can't do:**
  - Final shapes and colours from `design/mascot.svg`, placed inside the existing groups
  - The tongue shape for the lip lick in `hungry`
  - Optional: bones on the arms if rotation alone looks stiff

## Constraints
- Never cover the checkout bar, prices, buttons or form fields.
- The mascot never delays a tap or a screen change.
- Reduce motion on: stay idle with blinking only.
- Vectors only; keep the `.riv` small.

## Plan
Claude fills this in during stage 2. Example rig (replace with your character's parts);
each group holds one placeholder shape named `<group>_ph`, and the artboard matches the
reference art's viewBox.

| group         | parent | pivot         | notes                              |
|---------------|--------|---------------|------------------------------------|
| `body`        | root   | bottom centre | squash and stretch on hops         |
| `head`        | body   | neck          |                                    |
| `eye_L`       | head   | eye centre    | blink = scale Y                    |
| `eye_R`       | head   | eye centre    | blink = scale Y                    |
| `mouth_happy` | head   | mouth centre  | one mouth group visible at a time  |
| `mouth_open`  | head   | mouth centre  | hungry, celebrate                  |
| `mouth_sad`   | head   | mouth centre  | sorry                              |
| `tongue`      | head   | mouth corner  | hidden except during the lip lick  |
| `arm_L`       | body   | shoulder      |                                    |
| `arm_R`       | body   | shoulder      |                                    |
| `spoon`       | arm_R  | grip          | visible only in `cooking`          |

Milestones: blink layer, then idle, hungry, happy, cooking, celebrate, sorry, itemAdded.

## Open questions
- What food does Bae sell (burgers, fries, desserts, desi)? This shapes the cooking
  animation and placeholder menu.
- Does Bae already have a logo, colours or fonts the app and mascot must match?
- What does the mascot look like and what is its name? (Fill in once the SVG is ready.)
