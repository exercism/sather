# Instructions

Netball training starts with laps. The coach makes each lap a little longer
than the last: the first is 100 metres, the second 110, the third 120, and
so on, ten metres more each time.

All three tasks go in the `WARM_UP_LAPS` class.

## 1. How far in total?

Given a number of laps, work out the total distance.

```sather
WARM_UP_LAPS::distance_run(3)
-- => 330
```

That is 100 + 110 + 120. Nought laps is nought metres.

## 2. How many laps to cover a distance?

Given a distance in metres, how many laps does it take before the total is
at least that far?

```sather
WARM_UP_LAPS::laps_to_reach(330)
-- => 3
WARM_UP_LAPS::laps_to_reach(331)
-- => 4
```

Nought metres needs no laps at all.

## 3. Which lap first gets long?

Given a distance in metres, which is the first lap that is *itself* longer
than that? Lap 1 is 100 metres, lap 2 is 110, and so on.

```sather
WARM_UP_LAPS::first_long_lap(115)
-- => 3
```

Lap 3 is 120 metres, which is the first over 115.
