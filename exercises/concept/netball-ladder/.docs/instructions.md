# Instructions

Your netball club needs its ladder worked out after each round.

All four tasks go in the `NETBALL_LADDER` class.

## 1. Ladder points

A win is worth 4 points and a draw 2. Losses are worth nothing.

```sather
NETBALL_LADDER::ladder_points(3, 1)
-- => 14
```

## 2. Goal difference

Goals scored minus goals let in. It may be negative.

```sather
NETBALL_LADDER::goal_difference(180, 205)
-- => -25
```

## 3. Whole quarters played

A quarter is 15 minutes. Given a number of minutes, how many whole quarters
is that?

```sather
NETBALL_LADDER::whole_quarters(38)
-- => 2
```

## 4. Minutes into the quarter

Given the same number of minutes, how far into the current quarter are we?

```sather
NETBALL_LADDER::minutes_into_quarter(38)
-- => 8
```
