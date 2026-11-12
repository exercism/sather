# Hints

## General

- Every task needs a variable to count laps with, and two of them need a
  second variable for a running total.
- Work out the length of lap number `n` as a fixed part plus ten for every
  lap number. Find the fixed part by checking that lap 1 comes out at 100.

## 1. How far in total?

- Start the running total at 0 and the lap counter at 1.
- Put the `until!` at the top, asking whether the counter has gone past the
  number of laps. Then nought laps runs the body no times and leaves the
  total at 0.
- Add the length of the lap to the total, then add 1 to `lap`. Forgetting
  the second of those is what makes a loop run forever.

## 2. How many laps to cover a distance?

- Again a running total, but this time the question `until!` asks is about
  the total rather than the lap number: has it reached the distance yet?
- Put it at the top. Then asking for 0 metres answers 0 laps without
  running a lap.
- The answer is the lap counter when the loop ends.

## 3. Which lap first gets long?

- Nothing is being added up here, so no running total is needed.
- Test the length of the current lap, and `break!` out when it is over the
  distance asked about.
- Whatever `lap` holds when the loop ends is the answer.
