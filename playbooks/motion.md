# Playbook: motion

For animations people watch rather than control much: hero and banner animations,
logo reveals, explainers, illustrated loops, splash screens, story scenes.

## Questions for the brief
- What should the viewer understand or feel by the end?
- What are the beats, in order, and roughly how long is each?
- Does it play once, loop, or loop after an intro?
- Which aspect ratios and sizes?
- Any text, and in which languages?
- Should anything react to the viewer (hover, scroll, tap)?
- Is the art done by hand later (art pass), or is the code-built art final?

## What goes in the brief
- **Storyboard table:** beat, time range, what happens, text on screen.
- **Total length** and whether it loops.
- **Sizes:** each aspect ratio to support.

## Skeleton (stage 2)
- One artboard per aspect ratio, or one artboard with layouts if the content can
  reflow.
- A named group for every element that moves (`logo`, `title`, `bg_shape_1`).
- A state machine that plays the intro and then the loop, if the brief has both.
- A view model only for what an app or page needs to control (e.g. `replay` trigger,
  `paused` boolean, text strings).

## Milestones (stage 3)
1. The layout of each beat's key pose, as still frames.
2. Each beat's motion, one milestone each.
3. Transitions between beats and overall rhythm.
4. Interactive touches, if the brief has any.
5. The other aspect ratios.

## Testing
- Capture every beat's key frame with `--advance` to its time, and review them in order
  like a storyboard.
- For loops, compare the first and last frame with `--compare` to check the seam.
- Capture each aspect ratio at the same beats.

## Rules
- Hold each key moment long enough to read: about 1 s, plus time for any text.
- One main action at a time; overlap secondary motion by a few frames for follow-through.
- Loops are seamless.
- With reduce motion on, show the final frame (or a calm still) instead of playing.
