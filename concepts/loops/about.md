# Loops

```sather
   loop
      ...
   end;
```

Sather has exactly one loop statement. There is no `while` and no `for`;
both are built out of `loop` and something that ends it.

## Variables

```sather
   total ::= 0;          -- declare, with a starting value
   total := total + 5;   -- assign
```

`::=` declares and takes the type from the value given. When a variable has
to exist before there is a value for it, declare it with a type instead:

```sather
   total : INT;
   total := 0;
```

A variable declared without a value starts as zero for `INT`, `false` for
`BOOL`, and void for a string or an object.

## Ending a loop

| Written | Ends the loop |
| --- | --- |
| `until!(q)` | when `q` is true |
| `while!(q)` | when `q` is false |
| `break!` | straight away |

All three may appear anywhere in the body, and a loop may use more than one.

```sather
   loop
      until!(n > last);      -- may run no times at all
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
