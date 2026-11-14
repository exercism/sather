# Instructions

The circus is putting together its acrobatics act. Each of the questions
the troupe asks has a smaller question of the same kind inside it, so each
answer is a routine that calls itself.

The stub gives you the `HUMAN_PYRAMID` class and a placeholder for each
routine. Replace each placeholder with the real body.

## 1. Count the acrobats

In a human pyramid the bottom row has as many acrobats as the pyramid has
rows. Each row above has one fewer, up to a single acrobat at the top.

`acrobats` takes the number of rows and returns how many acrobats are needed
altogether. A pyramid with no rows needs nobody.

```sather
HUMAN_PYRAMID::acrobats(3)
-- => 6
```

A pyramid of three rows is a bottom row of three with a pyramid of two rows
standing on it.

## 2. Climb the rope ladder

The trapeze artist climbs a rope ladder to the platform, going up either one
rung or two rungs at each step. Climbing four rungs as 1, 1, 2 is a
different way from 2, 1, 1.

`ladder_ways` takes the number of rungs and returns how many different ways
there are to climb them. It is always given at least one rung.

```sather
HUMAN_PYRAMID::ladder_ways(3)
-- => 3
```

The three ways are 1, 1, 1 and 1, 2 and 2, 1.

## 3. Balance the see-saw

For the see-saw act, a group of acrobats on one end has to weigh exactly as
much as the performer on the other end.

`can_balance` takes the acrobats' weights, a position `from`, and a target
weight. It answers whether some of the acrobats at position `from` or later
weigh exactly `target` between them. Each acrobat can only be used once,
and a target of nought needs nobody.

```sather
HUMAN_PYRAMID::can_balance(|50, 40, 30|, 0, 70)
-- => true
HUMAN_PYRAMID::can_balance(|50, 40, 30|, 0, 60)
-- => false
```

The first one balances with the acrobats weighing 40 and 30.
