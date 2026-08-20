# Strings

A **string** is a piece of text. Sather's type for one is `STR`, and a
string is written between double quotes.

```sather
   composer : STR is
      return "Sibelius";
   end;
```

## Joining strings

`+` joins two strings end to end.

```sather
"Jean" + " " + "Sibelius"      -- "Jean Sibelius"
```

Nothing is put between them, so a space has to be asked for. Leaving it out
gives `"JeanSibelius"`.

## How long is it?

`.size` is how many characters a string holds. That is a whole number, so
its type is `INT`.

```sather
"Sibelius".size      -- 8
```

There are no brackets after `.size`, the same as a routine that takes no
arguments.

## Taking a piece

`.head(n)` is the first `n` characters. `.tail(n)` is the last `n`.

```sather
"Sibelius".head(3)   -- "Sib"
"Sibelius".tail(4)   -- "lius"
```

`head` counts from the front, `tail` counts from the back. Both leave the
original string alone and hand back a new one.
