# Project brief — Download button

## Project
- **Kind:** ui
- **What we're building:** a download button that shows progress and the result in
  place, for a file-sharing app
- **Goal:** users always know what the download is doing without a separate dialog
- **Audience:** app users on phones and tablets
- **Status:** production

## Look and feel
- **Reference art:** `design/download-button.png` (mockup of each state)
- **Style:** clean, calm, confident
- **Colours and fonts:** brand blue `#FF2F6FED`, success green, error red; system font
- **Art plan:** code-built art is final

## Rive names
- Rive file: `download_button` (CLI project in `rive/download_button/`)
- Artboard: `DownloadButton`
- State machine: `DownloadButtonSM`
- View model: `DownloadButtonVM`
  - `status` (enum): `idle`, `downloading`, `success`, `error`, `disabled`
  - `progress` (number, 0–1)
  - `label` (string): text on the button
  - `pressed` (trigger, out): the app listens for this to start the download

## Behaviour
| component      | states                                           | data in            | events out |
|----------------|--------------------------------------------------|--------------------|------------|
| DownloadButton | idle, hover, pressed, downloading, success, error, disabled | progress, label | pressed    |

- idle: arrow icon and label
- downloading: the button fills from left to right with `progress`; the arrow becomes a
  spinner
- success: a checkmark draws in, then returns to idle after 2 s
- error: a short shake, then a "Retry" label
- hover and pressed come from the pointer, not the view model

Sizes: 160 × 48, 240 × 56, and full width (the button stretches; the icon stays left).

Accessibility: role button; label follows `label`; announces "Downloading, N percent"
and "Download complete" or "Download failed".

## Inputs and events
- user taps the button → fire `pressed`
- app reports progress → set `progress`, `status = downloading`
- download finishes → `status = success`; fails → `status = error`

## Delivery
- **Where it goes:** a Flutter app in `app/`
- **Details:** a demo screen with buttons to simulate progress, success and error

## Constraints
- Press feedback within 100 ms.
- Works in light and dark mode.
- Reduce motion on: no shake; fill and checkmark appear without movement.

## Plan
Claude fills this in during stage 2 (groups, milestones, tests).

## Open questions
- Should the user be able to cancel during `downloading`?
