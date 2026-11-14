# Loops

A **loop** does the same thing over and over.

```sather
   loop
      ...
   end;
```

On its own that never stops, so something inside has to end it.

## Somewhere to keep count

A loop nearly always needs a variable that changes as it goes. Make it
before the loop starts, so that it keeps its value from one time round to
the next:

```sather
   total ::= 0;
```

Inside the loop, `:=` puts the new value back each time:

```sather
   total := total + 5;
```

## until!

`until!` takes a question. Each time round it is asked, and when the answer
is true the loop stops there and then.

```sather
   trips(waiting, per_trip : INT) : INT is
      count ::= 0;
      left ::= waiting;
      loop
         until!(left <= 0);
         left := left - per_trip;
         count := count + 1;
      end;
      return count;
   end;
```

A lift takes `per_trip` people at a time, and `trips` counts how many runs
it makes to carry everyone waiting. For `trips(10, 4)`, `left` goes 10, 6,
2, -2, and the loop ends the first time nobody is left: 3 trips. Without the
`left := left - per_trip` the question would never change its answer and the
loop would run forever.

`until!` does not have to be the first line. Put it where the question makes
sense: at the top, the loop may run no times at all; at the bottom, it
always runs at least once.

The `!` is part of the name. Sather marks certain things that way; what the
mark means comes later.

## break!

`break!` ends the loop immediately, with no question attached. It is useful
when the reason to stop turns up in the middle of the work.

```sather
   loop
      if doors_open then break!; end;
      ...
   end;
```

`until!` and `break!` only mean anything inside a `loop`. Neither can be
used on its own.
