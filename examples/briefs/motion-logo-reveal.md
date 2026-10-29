# Project brief — Logo reveal

## Project
- **Kind:** motion
- **What we're building:** a logo reveal for the top of a studio's landing page, which
  then settles into a gentle loop
- **Goal:** a confident first impression in under 4 seconds
- **Audience:** visitors to the studio's website
- **Status:** production

## Look and feel
- **Reference art:** `design/logo.svg`, every letter and the mark in their own named
  groups
- **Style:** precise and playful; a little overshoot, nothing bouncy
- **Colours and fonts:** from the logo; background transparent
- **Art plan:** placeholders now, art pass in the Rive Editor later

## Rive names
- Rive file: `logo_reveal` (CLI project in `rive/logo_reveal/`)
- Artboards: `Wide` (1600 × 600), `Square` (800 × 800)
- State machine: `RevealSM` (intro, then loop)
- View model: `RevealVM`
  - `replay` (trigger): play the intro again

## Behaviour
| beat | time      | what happens                                  | text on screen |
|------|-----------|-----------------------------------------------|----------------|
| 1    | 0.0–0.8 s | the mark draws in from its centre             |                |
| 2    | 0.8–1.8 s | letters rise into place, staggered 60 ms      | studio name    |
| 3    | 1.8–2.6 s | tagline fades up; the mark settles with a nod | tagline        |
| loop | 2.6 s +   | the mark breathes slowly (4 s loop)           |                |

## Inputs and events
- hover over the mark → a small tilt toward the pointer
- page script fires `replay` → intro plays again

## Delivery
- **Where it goes:** a `.riv` file for the web team
- **Details:** they embed it with Rive's web runtime at both sizes

## Art pass
- **Who:** the studio's designer, after stage 5
- **Tasks the placeholders can't do:** final logo shapes from `design/logo.svg`; the
  mark's draw-in as a stroke trim, if the art supports it

## Constraints
- Under 50 KB.
- Reduce motion on: show the final frame, no loop.

## Plan
Claude fills this in during stage 2 (groups, milestones, tests).

## Open questions
- Does the tagline change per page, so it should be a view model string?
