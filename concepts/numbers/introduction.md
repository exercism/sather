# Numbers

`INT` is Sather's type for whole numbers: `0`, `7`, `-3`. A routine that
answers with a whole number says so after the colon, the same way a routine
answering with text says `STR`.

```sather
   patients : INT is
      return 42;
   end;
```

Routines can take **arguments** — values handed in when the routine is
called. Each argument is named and given a type, in brackets after the
routine name:

```sather
   dose(kilos : INT, per_kilo : INT) : INT is
      return kilos * per_kilo;
   end;
```

When two arguments have the same type you may name them together:

```sather
   dose(kilos, per_kilo : INT) : INT is
```

Call it by putting the values in brackets:

```sather
VET::dose(4, 3)     -- this is 12
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

## Picking out bits

Inside the computer an `INT` is stored in binary, as a row of **bits**,
each a `1` or a `0`. Counting from nought at the right-hand end, bit `0`
stands for 1, bit `1` for 2, bit `2` for 4, bit `3` for 8, and so on, each
worth twice the one before. `5` is `4 + 1`, so it is `101` in binary: bits
`2` and `0` are set and bit `1` is not.

`.bit(i)` asks whether bit `i` is set, and answers `true` or `false`:

```sather
5.bit(0)     -- true
5.bit(1)     -- false
5.bit(2)     -- true
12.bit(3)    -- true, because 12 is 8 + 4
```

This is how a single number can carry several yes-or-no facts at once, one
per bit.

## Keeping a value

A routine can work something out, keep it under a name, and use it later.
That name is a **variable**, and `::=` makes one:

```sather
   weekly_dose(kilos, per_kilo : INT) : INT is
      daily ::= kilos * per_kilo;
      return daily * 7;
   end;
```

`daily` holds the answer to `kilos * per_kilo`. Sather works out from that
value that `daily` is an `INT`, so the type does not need writing. A
variable lasts until the end of the routine it was made in.

`:=` puts a new value into a variable that already exists:

```sather
   tablets ::= 20;
   tablets := tablets - 3;     -- tablets is now 17
```

Read the second line right to left: take what `tablets` is now, take away
3, and put the answer back into `tablets`.

Variables work the same way for any type: `name ::= "Rex";` makes a `STR`.

A few words belong to Sather and cannot be used as names. The one most
often tried is `result`, which Sather keeps for talking about a routine's
answer.
