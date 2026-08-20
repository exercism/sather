# Strings

`STR` holds text. A string is written between double quotes.

```sather
   composer : STR is
      return "Sibelius";
   end;
```

A `STR` never changes once it exists. Everything below answers with a *new*
string rather than altering the one it was asked about.

## Joining

```sather
"Jean" + " " + "Sibelius"      -- "Jean Sibelius"
```

`+` will also join a number onto a string, which is how a number gets into
a sentence:

```sather
"Opus " + 27           -- "Opus 27"
```

## Length

```sather
"Sibelius".size        -- 8
"".size                -- 0
```

`.size` counts characters, and the answer is an `INT`.

## Pieces

| Call | Answer |
| --- | --- |
| `"Sibelius".head(3)` | `"Sib"` |
| `"Sibelius".tail(4)` | `"lius"` |

Asking for more than there is gives back what there is, rather than
failing.

## Comparing

`=` asks whether two strings are the same text, and `/=` whether they
differ.

```sather
"forte" = "forte"      -- true
"forte" = "Forte"      -- false
```

Case matters. `.upper` and `.lower` give a copy in one case, which is the
usual way to compare without caring:

```sather
"Forte".lower                    -- "forte"
"Forte".lower = "forte".lower    -- true
```

## A word about size

A `STR` is a row of bytes, and `.size` counts bytes. For English text that
is the same as counting letters. For text with accents or other alphabets
it is not, because those letters take more than one byte each.
