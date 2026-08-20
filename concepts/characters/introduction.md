# Characters

A **character** is a single letter, digit, space or mark. Sather's type for
one is `CHAR`, and a character is written between single quotes.

```sather
   initial : CHAR is
      return 'M';
   end;
```

Single quotes for one character, double quotes for a string. `'M'` and
`"M"` are different types and cannot be swapped.

## Characters out of a string

A string is a row of characters, and square brackets reach one by position,
counting from nought — the same as an array.

```sather
"Marlowe"[0]      -- 'M'
"Marlowe"[3]      -- 'l'
```

## Asking about a character

| Call | Answers |
| --- | --- |
| `c.is_alpha` | is it a letter? |
| `c.is_digit` | is it one of `0`–`9`? |
| `c.is_upper` | is it a capital? |
| `c.is_lower` | is it a small letter? |

Each answers `true` or `false`.

```sather
'M'.is_alpha      -- true
'7'.is_alpha      -- false
'7'.is_digit      -- true
```

## Changing case

`.upper` gives the capital of a letter, and `.lower` the small one.
Anything that is not a letter is handed back unchanged.

```sather
'm'.upper         -- 'M'
'M'.lower         -- 'm'
'7'.upper         -- '7'
```

## Characters as numbers

Every character has a number. `.int` gives it, and `.char` turns a number
back into a character.

```sather
'a'.int           -- 97
'b'.int           -- 98
98.char           -- 'b'
```

The exact numbers rarely matter. What matters is that the letters `a` to
`z` are in order and next to each other, so `'c'.int - 'a'.int` is 2 — how
far `c` is along the alphabet. That is what makes a cipher wheel work.
