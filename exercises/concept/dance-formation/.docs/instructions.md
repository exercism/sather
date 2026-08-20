# Instructions

The dance troupe lines up in rows, and you are keeping track of who stands
where.

All five tasks go in the `DANCE_FORMATION` class.

## 1. How many in the row?

```sather
DANCE_FORMATION::dancer_count(|"Mia", "Ana", "Ben"|)
-- => 3
```

## 2. Who leads?

The leader is whoever stands first.

```sather
DANCE_FORMATION::leader(|"Mia", "Ana", "Ben"|)
-- => "Mia"
```

## 3. Who is at the back?

The back marker is whoever stands last, however long the row is.

```sather
DANCE_FORMATION::back_marker(|"Mia", "Ana", "Ben"|)
-- => "Ben"
```

## 4. The opening formation

The troupe always opens in the same order: Mia, Ana, Ben. Return that row.

```sather
DANCE_FORMATION::opening_row
-- => an array holding "Mia", "Ana" and "Ben", in that order
```

This routine takes no arguments.

## 5. Count the steps

Each dancer has a number of steps to do. Add them up.

```sather
DANCE_FORMATION::total_steps(|8, 16, 8|)
-- => 32
```

An empty row is nought steps.
