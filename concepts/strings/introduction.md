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
