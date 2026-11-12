# Custom Iterators

You have been using iterators since `bird-survey`. Now you write one.

## yield

An iterator looks like a routine with two differences: its name ends in `!`,
and it hands over values with `yield` instead of `return`.

```sather
   rising!(start : INT) : INT is
      size ::= start;
      loop
         yield size;
         size := size * 2;
      end;
   end;
```

`yield` gives a value to the loop that called the iterator, and then
**waits**. When that loop comes round again, the iterator carries on from
just after the `yield`, with everything exactly as it left it — its
variables, its own loop, its place.

That is what an iterator is: a routine that can pause in the middle and be
resumed. A dough that doubles in size every hour is 50, then 100, then 200,
and `size` remembers where it had got to:

```sather
   loop
      3.times!;
      #OUT + BAKERY::rising!(50) + " ";
   end;
   -- 50 100 200
```

`rising!` never ends by itself; the loop here stops when `times!` does.

## Ending

An iterator ends in either of two ways.

**Running out.** When the iterator's own loop finishes, or the routine
reaches its end, it is over — and the loop that called it ends immediately.

**quit.** `quit` ends it there and then, without yielding.

```sather
   fits!(trays : ARRAY{INT}, room : INT) : INT is
      used ::= 0;
      loop
         tray ::= trays.elt!;
         used := used + tray;
         if used > room then quit; end;
         yield tray;
      end;
   end;
```

That yields the sizes of trays going into an oven until the next one would
not fit, and stops. Running out of trays first ends it too. `quit` is to an
iterator what `return` is to a routine, except that it carries no value —
there is nothing left to hand over.

## once

An argument marked `once` is worked out one time only, when the loop starts,
rather than every time round:

```sather
   rising!(once start : INT) : INT is
```

Use it for anything that does not change between turns, which is most
arguments. The library's own iterators do: `upto!(once i : SAME)`.

## Iterators with no value

An iterator need not yield anything. `times!` is one:

```sather
   batches!(once count : INT) is
      loop
         ignored ::= 1.upto!(count);
         yield;
      end;
   end;
```

A bare `yield` hands over nothing and simply lets the loop go round.

## Where the position lives

Each *place in the program* that calls an iterator keeps its own position —
which is why calling the same iterator twice in one loop body walks it twice
over. Now you can see why: the two calls are two separate paused routines.
