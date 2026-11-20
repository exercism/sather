# Strings

A **string** is a piece of text. Sather's type for one is `STR`, and a
string is written between double quotes.

```sather
   street : STR is
      return "Collins";
   end;
```

## Joining strings

`+` joins two strings end to end.

```sather
"Collins" + " " + "Street"     -- "Collins Street"
```

Nothing is put between them, so a space has to be asked for. Leaving it out
gives `"CollinsStreet"`.

## How long is it?

`.size` is how many characters a string holds. That is a whole number, so
its type is `INT`.

```sather
"Collins".size       -- 7
```

There are no brackets after `.size`, the same as a routine that takes no
arguments.

## Taking a piece

`.head(n)` is the first `n` characters. `.tail(n)` is the last `n`.

```sather
"Collins".head(4)    -- "Coll"
"Collins".tail(3)    -- "ins"
```

`head` counts from the front, `tail` counts from the back. Both leave the
original string alone and hand back a new one.

## Finding text

`.search(s)` looks for `s` inside a string and answers where it starts, as
an `INT`. Positions are counted from `0`, so the first character is at `0`,
the second at `1`, and so on.

```sather
"Collins Street".search("Street")    -- 8
"Collins Street".search("C")         -- 0
"Collins Street".search("Lane")      -- -1
```

When `s` is not there at all, the answer is `-1`, which can never be a
position. If `s` turns up more than once, `search` answers with the first
place it starts.

Capitals have to match exactly: `"Collins Street".search("street")` is
`-1`.

## Numbers into strings

`.str` gives the text form of a number.

```sather
27.str               -- "27"
```

`+` does that for you when a number is joined onto the end of a string:

```sather
"Route " + 27        -- "Route 27"
```

The string has to come first. `27 + " trams"` does not compile, because `+`
on an `INT` expects another number. Write `27.str + " trams"` instead.

## Printing

`#OUT` is the screen. `+` onto it writes there, and more can be chained on
the same line:

```sather
   #OUT + "Route " + 27 + "\n";      -- prints Route 27
```

`"\n"` ends the line. Without it, the next thing printed carries on from
where this one stopped.

Printing is handy for seeing what a routine is doing while you work on it.
The tests only look at what a routine returns, so take the printing out
again when you are done.

## No string at all

A `STR` can also be **void**, which means there is no string there at all.
`void` is how you write that.

```sather
   suburb : STR is
      return void;      -- this address has no suburb
   end;
```

`void(x)` asks whether `x` is void, and answers `true` or `false`.

```sather
void(suburb)         -- true
void("")             -- false
void("Collins")      -- false
```

An empty string `""` is still a string, just one with no characters in it.
Void is no string at all.
