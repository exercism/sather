# Instructions

A violin is tuned by ear against a reference note. The strings sit a long
way apart in pitch, and the numbers involved are not whole ones.

All five tasks go in the `TUNING_THE_STRINGS` class.

## 1. Up an octave

A note an octave higher is twice the frequency.

```sather
TUNING_THE_STRINGS::octave_up(440.0d)
-- => 880.0d
```

## 2. Down an octave

An octave lower is half.

```sather
TUNING_THE_STRINGS::octave_down(440.0d)
-- => 220.0d
```

## 3. Halfway between

Given two frequencies, return the one exactly between them.

```sather
TUNING_THE_STRINGS::midpoint(440.0d, 442.0d)
-- => 441.0d
```

## 4. How far out?

When two notes are close but not the same, you hear a beat once a second
for every cycle they differ by. Return how far apart the frequencies are.
The answer is never negative, whichever note is higher.

```sather
TUNING_THE_STRINGS::beats_per_second(441.5d, 440.0d)
-- => 1.5d
```

## 5. Sharing out practice

Given a number of minutes and a number of players, how many minutes does
each get? The minutes and the players are whole numbers, but the answer may
not be.

```sather
TUNING_THE_STRINGS::minutes_each(45, 2)
-- => 22.5d
```
