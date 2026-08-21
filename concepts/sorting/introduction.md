# Sorting

Putting things in order is common enough that the library does it for you.

```sather
   scores : ARRAY{INT} := |3, 1, 2|;
   scores.sort;              -- 1, 2, 3
```

`sort` works on anything that already knows how to compare itself — numbers
and strings do, because they have an `is_lt`.

## Sorting by your own rule

Most orders are not the built-in one. A netball ladder is not alphabetical
and not by name length: it is by points, and then by goal difference for
teams level on points. There is no way for `ARRAY` to guess that.

So you hand the order in, as a bound routine:

```sather
   before(a, b : STR) : BOOL is
      return a.size < b.size;
   end;

   ...

   words.insertion_sort_by(bind(before(_, _)));
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
   -- shortest first
   return a.size < b.size;

   -- longest first: turn it round
   return a.size > b.size;
```

For a rule with more than one part, deal with the parts in order of
importance:

```sather
   higher(a, b : TEAM) : BOOL is
      if a.points /= b.points then
         return a.points > b.points;      -- more points comes first
      end;
      return a.difference > b.difference; -- level: better difference wins
   end;
```

The first `if` settles it whenever the points differ. Only when they are
equal does the second line get a say. Writing the tie-breaker first would
mean the points never mattered.

## Sorting changes the array

`insertion_sort_by` puts the array itself in order and answers nothing:

```sather
   teams.insertion_sort_by(bind(higher(_, _)));   -- teams is now sorted
```

If the original order matters, sort a copy:

```sather
   ranked ::= teams.copy;
   ranked.insertion_sort_by(bind(higher(_, _)));
   return ranked;
```
