# Sorting

Putting things in order is common enough that the library does it for you.

```sather
   orbits : ARRAY{INT} := |3, 1, 2|;
   orbits.sort;              -- 1, 2, 3
```

`sort` works on anything that already knows how to compare itself — numbers
and strings do, because they have an `is_lt`.

## Sorting by your own rule

Most orders are not the built-in one. Say a `PLANET` knows its `distance`
from the sun and its number of `moons`. Planets might be wanted nearest
first, or by how many moons they have, and neither is the order of their
names. There is no way for `ARRAY` to guess which.

So you hand the order in, as a bound routine:

```sather
   nearer(a, b : PLANET) : BOOL is
      return a.distance < b.distance;
   end;

   ...

   planets.insertion_sort_by(bind(nearer(_, _)));
```

`insertion_sort_by` takes a `ROUT{T,T}:BOOL` — a routine taking two of the
things being sorted and answering whether the first belongs before the
second. It calls that routine as often as it needs to and puts the array in
the order the answers imply.

This is what `understudy` was for. The library knows how to sort and nothing
about your idea of order; the bound routine is where the two meet.

## Writing the comparison

The routine answers **true when the first argument comes first**.

```sather
   -- nearest first
   return a.distance < b.distance;

   -- furthest first: turn it round
   return a.distance > b.distance;
```

For a rule with more than one part, deal with the parts in order of
importance:

```sather
   more_moons(a, b : PLANET) : BOOL is
      if a.moons /= b.moons then
         return a.moons > b.moons;    -- more moons comes first
      end;
      return a.distance < b.distance; -- level: nearer first
   end;
```

The first `if` settles it whenever the moons differ. Only when they are
equal does the second line get a say. Writing the tie-breaker first would
mean the moons never mattered.

## Sorting changes the array

`insertion_sort_by` puts the array itself in order and answers nothing:

```sather
   planets.insertion_sort_by(bind(nearer(_, _)));   -- planets is now sorted
```

If the original order matters, sort a copy instead. `.copy` answers a new
array holding the same elements, and sorting it leaves the first alone:

```sather
   spare ::= planets.copy;
```
