# Numbers

`INT` holds a whole number. In this Sather it is exactly 32 bits, so it
counts from -2147483648 to 2147483647.

```sather
   patients : INT is
      return 42;
   end;
```

## Arguments

A routine takes arguments in brackets, each with a type:

```sather
   dose(kilos : INT, per_kilo : INT) : INT is
      return kilos * per_kilo;
   end;
```

Arguments that share a type can share the declaration, which is the usual
style:

```sather
   dose(kilos, per_kilo : INT) : INT is
```

## Arithmetic

| Operator | Meaning |
| --- | --- |
| `+` | add |
| `-` | subtract, and negate |
| `*` | multiply |
| `/` | divide, discarding the remainder |
| `%` | the remainder of that division |

`/` between two `INT`s never produces a fraction:

```sather
7 / 2      -- 3
7 % 2      -- 1
```

If you want a fraction you need `FLTD`, which comes later.

Multiplication and division bind more tightly than addition and subtraction,
as in ordinary arithmetic. Brackets group when you need something else:

```sather
2 + 3 * 4        -- 14
(2 + 3) * 4      -- 20
```

## Variables

```sather
   daily ::= kilos * per_kilo;     -- make one; the type comes from the value
   daily := daily + 1;             -- give it a new value
```

The type can also be written out, with or without a starting value:

```sather
   tablets : INT := 20;
   left : INT;                     -- starts at 0
   morning, evening : INT;         -- two at once
```

A variable given no value starts as `0` for an `INT`, `false` for a `BOOL`,
and void for a `STR`. `::=` always needs a value with a type, so
`x ::= void;` is rejected; write `x : STR;` instead.

A variable lasts until the end of the routine that made it. Its type never
changes: `tablets := "none";` does not compile.

Sather's own words cannot be used as names. That includes `result`, which
is an ordinary name in many other languages. In Sather it means the
routine's answer, and postconditions use it.

## Useful routines on INT

```sather
7.max(3)     -- 7
7.min(3)     -- 3
(-7).abs     -- 7
7.str        -- "7", the number written as text
```

## Bits

`.bit(i)` is `true` when bit `i` of the number's binary form is `1`. Bit `0`
is the lowest, worth 1; bit `i` is worth 2 to the power `i`.

```sather
5.bit(0)     -- true:  5 is binary 101
5.bit(1)     -- false
5.bit(2)     -- true
```

A number used this way is a set of flags: each bit says yes or no to one
thing, and `.bit` reads one flag without any division or remainder.

`.str` is how a number becomes part of a sentence, once you have met
strings.
