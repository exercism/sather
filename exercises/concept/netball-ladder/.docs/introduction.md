# Numbers

`INT` is Sather's type for whole numbers: `0`, `7`, `-3`. A routine that
answers with a whole number says so after the colon, the same way a routine
answering with text says `STR`.

```sather
   goals : INT is
      return 42;
   end;
```

Routines can take **arguments** — values handed in when the routine is
called. Each argument is named and given a type, in brackets after the
routine name:

```sather
   total(first : INT, second : INT) : INT is
      return first + second;
   end;
```

When two arguments have the same type you may name them together:

```sather
   total(first, second : INT) : INT is
```

Call it by putting the values in brackets:

```sather
SCORES::total(3, 4)     -- this is 7
```

The five arithmetic operators are `+`, `-`, `*`, `/` and `%`.

`/` on two `INT`s is **integer division**: it throws away any remainder
rather than giving a fraction.

```sather
7 / 2      -- 3, not 3.5
```

`%` gives what is left over from that division.

```sather
7 % 2      -- 1
```

The two go together: `7` is `3` lots of `2` with `1` left over.
