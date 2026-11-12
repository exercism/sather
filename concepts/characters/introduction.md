# Characters

A **character** is a single letter, digit, space or mark. Sather's type for
one is `CHAR`, and a character is written between single quotes.

```sather
   knit : CHAR is
      return 'k';
   end;
```

Single quotes for one character, double quotes for a string. `'k'` and
`"k"` are different types and cannot be swapped.

## Characters out of a string

A string is a row of characters, and square brackets reach one by position,
counting from nought — the same as an array.

```sather
"K2P2"[0]         -- 'K'
"K2P2"[1]         -- '2'
```

That is a row of a knitting pattern: knit two, purl two.

## Asking about a character

| Call | Answers |
| --- | --- |
| `c.is_alpha` | is it a letter? |
| `c.is_digit` | is it one of `0`–`9`? |
| `c.is_upper` | is it a capital? |
| `c.is_lower` | is it a small letter? |

Each answers `true` or `false`.

```sather
'P'.is_alpha      -- true
'2'.is_alpha      -- false
'2'.is_digit      -- true
```

## Changing case

`.upper` gives the capital of a letter, and `.lower` the small one.
Anything that is not a letter is handed back unchanged.

```sather
'p'.upper         -- 'P'
'P'.lower         -- 'p'
'2'.upper         -- '2'
```

## Characters as numbers

Every character has a number. `.int` gives it, and `.char` turns a number
back into a character.

```sather
'k'.int           -- 107
'p'.int           -- 112
112.char          -- 'p'
```

The exact numbers rarely matter. What matters is that the letters `a` to
`z` are in order and next to each other, so `'p'.int - 'k'.int` is 5 — how
many letters `p` comes after `k`. The digits `0` to `9` are in order too,
so `'2'.int - '0'.int` is 2, the number a digit character stands for.
