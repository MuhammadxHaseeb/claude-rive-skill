# Playbook: character

For mascots, avatars, guides and other characters that react to an app or a user.

## Questions for the brief
- Who is the character: personality, look, name? Is there reference art in `design/`?
- Where does it appear, and how large?
- Which moods or states does it have, and which app moments trigger each one?
- Which one-shot reactions (a hop, a nod, a wave), and what does each return to?
- Should anything play over every state (blinking, breathing)?
- What must it never cover or delay?
- Is the art done by hand later (art pass), or is the code-built art final?

## What goes in the brief
- **Behaviour:** a states table (mood, app moment, animation), the one-shot reactions,
  and the ambient layer.
- **Inputs and events:** app event → view model change.
- **Plan (stage 2):** a rig table (group, parent, pivot, notes), one row per moving
  part, filled in from the reference art.

## Skeleton (stage 2)
- One artboard sized to the reference art.
- The rig: a named group per moving part, nested as in the rig table, each with its
  pivot set (arms at the shoulder, head at the neck, body at its base, eyes at their
  centre). Expressions that change a part's shape get one sibling group per variant
  (`mouth_happy`, `mouth_sad`).
- One view model: an enum for the main state (the "mood"), triggers for one-shot
  reactions, numbers or booleans only where the brief asks.
- One state machine with a state for every mood, plus a separate layer for ambient
  motion.

## Milestones (stage 3)
1. The ambient layer (e.g. blinking).
2. Each mood and one-shot reaction, one milestone each, in the order the brief lists
   them.

## Testing
- For each mood, set it with `--data`, step through the loop with `--advance` and
  capture a few frames, including the first and last to check the loop is seamless.
- For each reaction, fire the trigger and capture the key poses and the return state.
- Check that ambient motion keeps running in every mood.

## Rules
- Loops: 2–4 s and seamless. One-shots: under 1.2 s, then return to the state the brief
  says.
- Blend transitions between states over 150–250 ms.
- Animate the rig's groups only (see "Swappable placeholders" in `CLAUDE.md`).
- With reduce motion on, stay in the idle state with only subtle ambient motion.
- The character never covers buttons, prices, form fields or other key UI, and never
  delays the user's main task.
