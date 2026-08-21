# Custom Iterators

```sather
   markers!(once spacing : INT, once count : INT) : INT is
      loop
         yield spacing * 1.upto!(count);
      end;
   end;
```

| | routine | iterator |
| --- | --- | --- |
| name | `foo` | `foo!` |
| hands back a value | `return` | `yield` |
| finishes | `return`, or the end | `quit`, or running out |
| may be called | anywhere | only inside a `loop` |
| keeps its place | no | yes |

## yield

`yield` hands over a value and suspends. Everything is restored on the next
turn: local variables, the position in the iterator's own loops, and the
positions of any iterators it is itself calling.

A `yield` inside nested loops resumes at the innermost one, which is what
makes writing a walk over something nested straightforward:

```sather
   all_cells!(grid : ARRAY{ARRAY{INT}}) : INT is
      loop
         row ::= grid.elt!;
         loop
            yield row.elt!;
         end;
      end;
   end;
```

## quit

Ends the iterator, and so the loop calling it. It carries no value: a `quit`
is not a last result, it is the announcement that there are none.

An iterator with a return type must `yield` a value every time it yields;
`quit` is how it declines to.

## once

```sather
   markers!(once count : INT) : INT is
```

A `once` argument is evaluated when the loop is entered and kept. A plain
argument is re-evaluated every turn, which matters when the expression
passed in contains another iterator call:

```sather
   loop
      #OUT + TRAIL::markers!(sizes.elt!);     -- a new count every turn
   end;
```

Mark arguments `once` unless you specifically want that. The whole library
does.

## self and iterators

An iterator may be called on an object, and then `self` is that object. Its
paused state belongs to the call site, not to the object, so two loops
walking the same object do not interfere.

## When to write one

Write an iterator when the answer is a sequence and the caller should decide
how much of it to take. It costs nothing to stop early, and nothing is built
that is not used — where a routine returning an `ARRAY` has to build the
whole thing first.
