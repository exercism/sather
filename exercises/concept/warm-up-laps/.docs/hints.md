# Hints

## General

- Every task needs a variable to count laps with, and two of them need a
  second variable for a running total.
- Lap number `n` is `90 + 10 * n` metres long. Check it: lap 1 gives 100.

## 1. How far in total?

- Start `total` at 0 and `lap` at 1.
- End the loop with `until!(lap > laps)` at the top, so that nought laps
  runs the body no times and leaves the total at 0.
- Add the length of the lap to the total, then add 1 to `lap`. Forgetting
  the second of those is what makes a loop run forever.

## 2. How many laps to cover a distance?

- Again a running total, but this time the question is about the total
  rather than the lap number: `until!(total >= metres)`.
- Put it at the top. Then asking for 0 metres answers 0 laps without
  running a lap.
- The answer is the lap counter when the loop ends.

## 3. Which lap first gets long?

- Nothing is being added up here, so no running total is needed.
- Test the length of the current lap, and `break!` out when it is over the
  distance asked about.
- Whatever `lap` holds when the loop ends is the answer.
