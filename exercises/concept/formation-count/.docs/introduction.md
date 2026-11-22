# Exact Numbers

Two of the number types you have met give up something.

`INT` is exactly 32 bits, so it holds numbers from about minus two billion
to two billion and no further. Those two ends are `INT::minval` and
`INT::maxval`. Go past either and the program stops with "Integer overflow".

`FLTD` holds fractions, but only approximately. `0.1d + 0.2d` is very nearly
`0.3` and not exactly.

For work where those matter, the library has a type each.

## INTI: whole numbers of any size

`INTI` holds a whole number with no limit but memory.

```sather
   #INTI(2).pow(100)
   -- 1267650600228229401496703205376
```

An `INT` cannot hold that. An `FLTD` could hold something close to it, and
would lose the last twenty digits.

Counting arrangements is the standard reason to want this. Twelve players
in a chess tournament can finish in 479001600 different orders, which an
`INT` holds; thirteen can finish in 6227020800, which it does not.

```sather
   #INTI(16).factorial
   -- 20922789888000
```

## Making numbers

Make one from an `INT`, or from a string when the number is too big to
write as an `INT` in the first place:

```sather
   #INTI(42)
   #INTI("123456789012345678901234567890")
```

Then `+`, `-`, `*`, `/` and comparison all work as usual, and `.str` gives
every digit.

An ordinary `INT` can be read from a string the same way, as long as the
number fits:

```sather
   #INT("42")             -- 42
   #INT("-17")            -- -17
```

`#INT` never complains. It reads as much of a number as it finds at the
start of the string and stops there, so `#INT("12 eggs")` is `12`, and a
string with no number at the start at all gives `0`.

## RAT: exact fractions

`RAT` holds one whole number over another, and keeps them that way.

```sather
   #RAT(3, 4)          -- 3/4, exactly
   #RAT(1, 4) + #RAT(2, 3)
   -- 11/12
```

No rounding happens, because nothing is ever converted to a decimal.

```sather
   #RAT(1, 10) + #RAT(2, 10) = #RAT(3, 10)      -- true
   0.1d + 0.2d = 0.3d                            -- not to be relied on
```

A `RAT` reduces itself: `#RAT(2, 4)` is `1/2`, and prints as `1/2`. One that
comes out whole prints as a whole number: `#RAT(6, 3)` prints `2`.

## The cost

Both are slower than the built-in types, and both allocate memory. `INT` and
`FLTD` are single machine instructions; `INTI` and `RAT` are objects doing
arithmetic in software.

Use them where exactness is the point, and the ordinary types everywhere
else.
