# Custom Iterators

You have been using iterators since `bird-survey`. Now you write one.

## yield

An iterator looks like a routine with two differences: its name ends in `!`,
and it hands over values with `yield` instead of `return`.

```sather
   markers!(count : INT) : INT is
      loop
         yield 100 * 1.upto!(count);
      end;
   end;
```

`yield` gives a value to the loop that called the iterator, and then
**waits**. When that loop comes round again, the iterator carries on from
just after the `yield`, with everything exactly as it left it — its
variables, its own loop, its place.

That is what an iterator is: a routine that can pause in the middle and be
resumed.

```sather
   loop
      #OUT + TRAIL::markers!(3) + " ";      -- 100 200 300
   end;
```

## Ending

An iterator ends in either of two ways.

**Running out.** When the iterator's own loop finishes, or the routine
reaches its end, it is over — and the loop that called it ends immediately.

**quit.** `quit` ends it there and then, without yielding.

```sather
   named!(names : ARRAY{STR}) : STR is
      loop
         name ::= names.elt!;
         if name = "" then quit; end;
         yield name;
      end;
   end;
```

That yields names until it meets an empty one, and stops. `quit` is to an
iterator what `return` is to a routine, except that it carries no value —
there is nothing left to hand over.

## once

An argument marked `once` is worked out one time only, when the loop starts,
rather than every time round:

```sather
   markers!(once count : INT) : INT is
```

Use it for anything that does not change between turns, which is most
arguments. The library's own iterators do: `upto!(once i : SAME)`.

## Iterators with no value

An iterator need not yield anything. `times!` is one:

```sather
   steps!(once count : INT) is
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
