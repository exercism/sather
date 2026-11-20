# Hints

## General

- None of these needs an `if`, a loop, or any arithmetic operator. Each is
  one or two bit routines.
- Tasks 3, 4 and 5 all need a rig with just the one light on. You wrote
  that in task 2, and you can call it.

## 1. Is this light on?

- `.bit` already answers this.

## 2. One light on its own

- The rig with only light `0` on is `1`. Every other answer is that `1`
  moved left.

## 3. Switch a light on

- A light should be on afterwards if it is on in the rig **or** it is the
  one being switched on.

## 4. Switch a light off

- First make a rig with every light on **except** this one: that is the
  opposite of task 2's answer.
- Then keep only the lights that are on in **both** that and the rig.

## 5. Flip a light

- Changing a bit wherever the other number has a `1` is exactly what
  `bxor` does.

## 6. The back row

- Shift the whole rig right by eight, so that light `8` lands on bit `0`.
- The foyer lights have moved down too. Keep only the bottom eight bits
  with `band`; the number with exactly those eight bits on is `255`.
