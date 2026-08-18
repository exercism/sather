# Numbers

`INT` holds a whole number. In this Sather it is exactly 32 bits, so it
counts from -2147483648 to 2147483647.

```sather
   goals : INT is
      return 42;
   end;
```

## Arguments

A routine takes arguments in brackets, each with a type:

```sather
   total(first : INT, second : INT) : INT is
      return first + second;
   end;
```

Arguments that share a type can share the declaration, which is the usual
style:

```sather
   total(first, second : INT) : INT is
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

## Useful routines on INT

```sather
7.max(3)     -- 7
7.min(3)     -- 3
(-7).abs     -- 7
7.str        -- "7", the number written as text
```

`.str` is how a number becomes part of a sentence, once you have met
strings.
