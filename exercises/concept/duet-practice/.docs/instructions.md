# Instructions

Two violinists are rehearsing a duet. Each part is an array holding the
number of notes in each bar, and the parts are not always the same length.

All four tasks go in the `DUET_PRACTICE` class.

## 1. How many bars do they play together?

They play together for as long as both parts have a bar left.

```sather
DUET_PRACTICE::bars_together(|4, 4, 8, 8|, |4, 4|)
-- => 2
```

## 2. How many bars match?

Count the bars where both parts have the same number of notes. Only bars
they both have can match.

```sather
DUET_PRACTICE::in_unison(|4, 4, 8|, |4, 2, 8|)
-- => 2
```

## 3. Who is busier?

Count the bars where the first part has more notes than the second.

```sather
DUET_PRACTICE::louder_bars(|4, 8, 2|, |4, 2, 8|)
-- => 1
```

## 4. Weight the bars

Later bars are harder, so a bar counts for as much as its position: the
first bar counts once, the second twice, the third three times. Multiply
each bar's notes by its number and add up the lot.

```sather
DUET_PRACTICE::weighted_total(|4, 4, 8|)
-- => 36
```

That is 1×4 + 2×4 + 3×8. Bars are numbered from one, not nought.
