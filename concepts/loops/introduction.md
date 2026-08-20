# Loops

A **loop** does the same thing over and over.

```sather
   loop
      ...
   end;
```

On its own that never stops, so something inside has to end it.

## Somewhere to keep count

A loop nearly always needs a value that changes as it goes. That is a
**variable**, and `::=` makes one:

```sather
   total ::= 0;
```

The variable is called `total`, it starts at `0`, and Sather works out from
the `0` that it holds an `INT`. After that, `:=` puts a new value in:

```sather
   total := total + 5;
```

Read that right to left: take what `total` is now, add 5, and put the answer
back into `total`.

A variable made this way lives until the end of the routine.

## until!

`until!` takes a question. Each time round it is asked, and when the answer
is true the loop stops there and then.

```sather
   sum_to(last : INT) : INT is
      total ::= 0;
      n ::= 1;
      loop
         until!(n > last);
         total := total + n;
         n := n + 1;
      end;
      return total;
   end;
```

`n` counts 1, 2, 3 ... and the loop ends the first time `n` is past `last`.
Without the `n := n + 1` the question would never change its answer and the
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
      if too_far then break!; end;
      ...
   end;
```

`until!` and `break!` only mean anything inside a `loop`. Neither can be
used on its own.
