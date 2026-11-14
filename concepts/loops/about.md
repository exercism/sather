# Loops

```sather
   loop
      ...
   end;
```

Sather has exactly one loop statement. There is no `while` and no `for`;
both are built out of `loop` and something that ends it.

## Variables

A variable that counts or collects is made before the loop, so that it
keeps its value from one time round to the next:

```sather
   total ::= 0;
   loop
      ...
      total := total + 5;
   end;
```

A `::=` inside the loop body runs every time round, so that variable is set
afresh each time. A variable declared in the body without a value, as in
`count : INT;`, is not: it carries on from the time before.

## Ending a loop

| Written | Ends the loop |
| --- | --- |
| `until!(q)` | when `q` is true |
| `while!(q)` | when `q` is false |
| `break!` | straight away |

All three may appear anywhere in the body, and a loop may use more than one.

```sather
   loop
      until!(left <= 0);     -- may run no times at all
      ...
   end;

   loop
      ...
      until!(done);          -- always runs at least once
   end;
```

## The exclamation mark

`until!`, `while!` and `break!` end in `!` because they are **iterators** —
things that may only appear inside a loop, and that can end it. Writing one
outside a loop is an error rather than a warning. Later exercises use the
library's other iterators, and eventually write new ones.

## Forever loops

A loop with nothing to end it runs forever. That is occasionally what is
wanted, but far more often it means the value the question asks about is
never changed. If a program hangs, the first thing to check is whether
something inside the loop moves it towards stopping.
