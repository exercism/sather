# Instructions

You are helping with a bird survey. Each day somebody sits at a hide and
counts what flies past, and the day's counts come back as an array.

All five tasks go in the `BIRD_SURVEY` class.

## 1. The total

Add up every day's count.

```sather
BIRD_SURVEY::total_seen(|3, 0, 7|)
-- => 10
```

A survey with no days at all counts nought birds.

## 2. The best day

Return the largest count. If there were no days, the answer is nought.

```sather
BIRD_SURVEY::busiest_day(|3, 0, 7|)
-- => 7
```

## 3. The busy days

How many days had a count above some number?

```sather
BIRD_SURVEY::days_over(|3, 0, 7|, 2)
-- => 2
```

Above means above: a count of exactly 2 does not count.

## 4. Hides to check

On the first day of the survey you check one hide, on the second day two,
and so on. How many hide checks is that altogether?

```sather
BIRD_SURVEY::hides_to_check(4)
-- => 10
```

That is 1 + 2 + 3 + 4.

## 5. The first busy day

Which day was the first with a count above some number? Days are numbered
from nought, the way array positions are. If no day was that busy, the
answer is `-1`.

```sather
BIRD_SURVEY::first_busy_day(|3, 0, 7|, 5)
-- => 2
BIRD_SURVEY::first_busy_day(|3, 0, 7|, 9)
-- => -1
```
