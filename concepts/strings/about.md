# Strings

`STR` holds text. A string is written between double quotes.

```sather
   street : STR is
      return "Collins";
   end;
```

A `STR` never changes once it exists. Everything below answers with a *new*
string rather than altering the one it was asked about.

## Joining

```sather
"Collins" + " " + "Street"     -- "Collins Street"
```

`+` will also join a number onto a string, which is how a number gets into
a sentence:

```sather
"Route " + 27          -- "Route 27"
```

## Length

```sather
"Collins".size         -- 7
"".size                -- 0
```

`.size` counts characters, and the answer is an `INT`.

## Pieces

| Call | Answer |
| --- | --- |
| `"Collins".head(4)` | `"Coll"` |
| `"Collins".tail(3)` | `"ins"` |

Asking for more than there is gives back what there is, rather than
failing.

## Comparing

`=` asks whether two strings are the same text, and `/=` whether they
differ.

```sather
"lane" = "lane"        -- true
"lane" = "Lane"        -- false
```

Case matters. `.upper` and `.lower` give a copy in one case, which is the
usual way to compare without caring:

```sather
"Lane".lower                      -- "lane"
"Lane".lower = "lane".lower      -- true
```

## A word about size

A `STR` is a row of bytes, and `.size` counts bytes. For English text that
is the same as counting letters. For text with accents or other alphabets
it is not, because those letters take more than one byte each.
