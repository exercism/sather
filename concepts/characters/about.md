# Characters

`CHAR` is one character, written between single quotes.

```sather
   c : CHAR := 'M';
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
'M'.is_alpha      -- true
'7'.is_digit      -- true
'M'.is_upper      -- true
' '.is_space      -- true
'M'.is_alphanum   -- true, a letter or a digit
```

## Case

`.upper` and `.lower` change a letter's case and leave everything else
alone, so they are safe to apply to a character you have not checked.

## Numbers

```sather
'a'.int           -- 97
97.char           -- 'a'
```

`.int` and `.char` are exact opposites. The useful facts about the numbering
are that `'a'` to `'z'` run consecutively, `'A'` to `'Z'` run consecutively,
and `'0'` to `'9'` run consecutively — so:

```sather
   c.int - 'a'.int          -- how far c is along the alphabet
   ('a'.int + n).char       -- the letter n places along
   d.int - '0'.int          -- the value of a digit character
```

## Wrapping round

A cipher wheel turns past `z` and back to `a`. `%` does exactly that:

```sather
   ('a'.int + (c.int - 'a'.int + places) % 26).char
```

Sather's `%` never answers negative when the right-hand side is positive, so
this works for turning the wheel backwards as well as forwards.

## Characters and strings

A `STR` is a row of bytes, and a `CHAR` is one byte. For English text a byte
is a letter, so `"Marlowe".size` is 7 and `"Marlowe"[0]` is `'M'`. For text
with accents or another alphabet, one letter may take several bytes, and
neither of those holds.
