---
name: rive-animations
description: Use when implementing Disney's 12 animation principles with Rive interactive animations
---

# Rive Animation Principles

Implement all 12 Disney animation principles using Rive's editor: timelines, the Graph
Editor, bones, constraints and state machines.

> Adapted for this template from dylantarre/animation-principles (MIT). The original's
> runtime code samples were removed because they used legacy APIs (`rive.play()`,
> state machine inputs). The app drives the animation only through view model data
> binding, as described in `CLAUDE.md`; follow that for anything runtime-related.

## In this template

The animation is written as RML with the Rive CLI, not built by hand in the Editor.
The Editor features named below (timelines, easing, layers, blend states) have RML
equivalents; look them up with `rive schema` and `rive docs --search`. Keyframe easing
replaces the Graph Editor.

When the brief plans an art pass, animate the named groups, never the placeholder
shapes inside them, and leave bones, meshes, IK and path animation to the art pass.
Where a principle below needs those (squash and stretch, arcs, follow-through), get the
same effect with group scale, rotation and keyframe offsets. See "Swappable
placeholders" in `CLAUDE.md`.

## 1. Squash and Stretch

In Rive Editor:
- Create shape with bones
- Animate scale X/Y with inverse relationship to preserve volume
- Key: `scaleX: 1.2` when `scaleY: 0.8`

## 2. Anticipation

- Add a short wind-up pose before the main action (crouch before a jump, lean back
  before a wave)
- Build it as the opening keys of the same animation, so one view model change or
  trigger plays wind-up → action in sequence

## 3. Staging

In Rive:
- Use artboard layers for depth
- Apply blur/opacity to background layers
- Use nested artboards for complex scenes
- Keep one clear action readable at a time

## 4. Straight Ahead / Pose to Pose

Pose to Pose in Rive:
- Set key poses on timeline
- Rive interpolates between
- Use easing curves in Graph Editor

## 5. Follow Through and Overlapping Action

In Rive Editor:
- Use bone hierarchy with constraints
- Apply "delay" or "lag" to child bones
- Or offset keyframes by 2-4 frames
- Use spring constraints for natural follow-through

## 6. Slow In and Slow Out

In Rive Graph Editor:
- Select keyframes
- Apply easing: Cubic, Quad, Bounce
- Adjust bezier handles for custom curves

## 7. Arc

In Rive:
- Use IK (Inverse Kinematics) for natural arcs
- Apply path constraints
- Animate position with curved interpolation

## 8. Secondary Action

- Add small supporting motion to a main action (ears flop as the body lands, eyes
  squint during a laugh)
- Put secondary motion that should play everywhere (blinking, breathing) on its own
  state machine layer so it runs over every state
- Use blend states to mix a secondary animation with the main one

## 9. Timing

In Rive Editor:
- Adjust animation duration and keyframe spacing: fewer frames feel snappy, more
  frames feel heavy or dramatic
- Use work area to fine-tune timing
- Graph Editor for precise control

## 10. Exaggeration

In Rive:
- Push bone rotations beyond natural limits
- Exaggerate scale transformations
- Use elastic/bounce interpolation
- Overshoot in Graph Editor curves

## 11. Solid Drawing

In Rive:
- Use multiple bones for volume preservation
- Apply constraints to maintain form
- Use clipping for depth illusion
- Layer shapes for 3D effect

## 12. Appeal

Design in Rive:
- Smooth bezier curves on shapes
- Consistent stroke weights
- Pleasing color palette
- Clean bone structure

## Key Rive Features

- **State Machines** - Logic-driven animation flow
- **Layers** - Run ambient animations over every state
- **Blend States** - Mix multiple animations
- **Listeners** - Pointer events in editor
- **Constraints** - IK, path, distance, rotation
- **Bones & Meshes** - Skeletal animation
- **Data Binding** - View model properties drive the state machine
- **Tiny file size** - Optimized binary format
