# Exact Numbers

Two of the number types you have met give up something.

`INT` is exactly 32 bits, so it holds numbers from about minus two thousand
million to two thousand million and no further. Go past that and it wraps
round silently — no error, just a wrong answer.

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

Make one from an `INT`, or from a string when the number is too big to
write as an `INT` in the first place:

```sather
   #INTI(42)
   #INTI("123456789012345678901234567890")
```

Then `+`, `-`, `*`, `/` and comparison all work as usual, and `.str` gives
every digit.

Counting the ways a troupe can line up is the standard reason to want this.
Twelve dancers have 479001600 ways, which an `INT` holds; thirteen have
6227020800, which it does not.

```sather
   #INTI(20).factorial
   -- 2432902008176640000
```

## RAT: exact fractions

`RAT` holds one whole number over another, and keeps them that way.

```sather
   #RAT(1, 3)          -- 1/3, exactly
   #RAT(1, 2) + #RAT(1, 3)
   -- 5/6
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
