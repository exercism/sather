# Characters

`CHAR` is one character, written between single quotes.

```sather
   c : CHAR := 'k';
```

## Special characters

Some characters cannot be typed directly and are written with a backslash:

| Written | Is |
| --- | --- |
| `'\n'` | a new line |
| `'\t'` | a tab |
| `'\''` | a single quote |
| `'\\'` | a backslash |

## Questions

```sather
'K'.is_alpha      -- true
'2'.is_digit      -- true
'K'.is_upper      -- true
' '.is_space      -- true
'K'.is_alphanum   -- true, a letter or a digit
```

## Case

`.upper` and `.lower` change a letter's case and leave everything else
alone, so they are safe to apply to a character you have not checked.

## Numbers

```sather
'k'.int           -- 107
107.char          -- 'k'
```

`.int` and `.char` are exact opposites. The useful facts about the numbering
are that `'a'` to `'z'` run consecutively, `'A'` to `'Z'` run consecutively,
and `'0'` to `'9'` run consecutively — so:

```sather
   d.int - '0'.int          -- the value of a digit character
   ('0'.int + n).char       -- the digit character for n, from 0 to 9
```

## Wrapping round

A knitting pattern repeats. Counting stitches from nought, stitch 9 of a row
worked from `"K2P2"` is the same as stitch 1, because the pattern is four
stitches long and starts again after each four. `%` does exactly that:

```sather
   pattern[stitch % pattern.size]      -- stitches counted from nought
```

Sather's `%` never answers negative when the right-hand side is positive:
`-1 % 4` is 3, not -1. So the same expression works counting backwards from
the start of a row as well as forwards.

## Characters and strings

A `STR` is a row of bytes, and a `CHAR` is one byte. For English text a byte
is a letter, so `"Purl".size` is 4 and `"Purl"[0]` is `'P'`. For text
with accents or another alphabet, one letter may take several bytes, and
neither of those holds.
