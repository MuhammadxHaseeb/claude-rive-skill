# Playbook: ui

For interactive UI pieces: buttons, toggles, loaders, progress bars, icons, cards,
onboarding screens, dashboards and other components an app drives with data.

## Questions for the brief
- Which components, and where are they used?
- Which states does each have (idle, hover, pressed, focused, disabled, loading,
  success, error)?
- What data does the app send in (progress, labels, counts, values)?
- Which sizes must it work at? Should it resize with its container?
- Light and dark themes? Brand colours and fonts?
- What should screen readers announce?
- Is the art done by hand later (art pass), or is the code-built art final?

## What goes in the brief
- **Components table:** component, states, data in, events out.
- **Sizes:** the viewport sizes to support.
- **Accessibility:** the label and role for each interactive part.

## Skeleton (stage 2)
- One artboard per component, using layouts so it resizes with its container.
- Named groups for each visual part (`bg`, `icon`, `label`, `progress_fill`).
- One view model per component: an enum for the state, numbers or strings for the data,
  triggers for events the app listens to.
- Text bound to view model strings, never outlined.
- A state machine per component with a state for each brief state.

## Milestones (stage 3)
1. Static layout at every size in the brief.
2. Each state, one milestone each.
3. Transitions between states and pointer feedback (hover, press).
4. Data binding for the values the app sends in.
5. Accessibility semantics.
6. Theming, if the brief asks for it.

## Testing
- Capture every state at every size: `--viewport` plus `--data` for the state.
- Simulate hover and press with `--pointer` and check the feedback.
- Set edge-case data: 0% and 100% progress, long labels, empty strings.
- Check what screen readers get with `--semantics`.

## Rules
- Press feedback starts within 100 ms; state transitions take 150–300 ms.
- UI motion never blocks or delays the user's task.
- Hit areas are at least 44 × 44 pt.
- With reduce motion on, switch states without movement (fades only).
