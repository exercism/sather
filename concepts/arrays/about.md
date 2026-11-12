# Arrays

`ARRAY{T}` is a fixed row of values of type `T`.

```sather
   shelf : ARRAY{STR} := |"Emma", "Dracula", "Kim"|;
   pages : ARRAY{INT} := |474, 418, 368|;
```

## The braces

`ARRAY{STR}` is read "array of `STR`". The braces hold a **type parameter**:
`ARRAY` on its own is not a type, because an array has to be an array of
something. Much of the Sather library is built this way, and writing such a
class yourself comes later.

## Positions

```sather
shelf[0]                 -- the first
shelf[shelf.size - 1]    -- the last
shelf.size               -- how many
```

Positions run from `0` to `.size - 1`. An array knows its size and never
changes it: there is no appending to an `ARRAY`.

## Making one without a literal

`#ARRAY{INT}(n)` makes an array of `n` values, each nought:

```sather
   loans ::= #ARRAY{INT}(5);      -- five noughts
   loans[0] := 7;
```

Assigning into a position uses the same square brackets on the left of
`:=`.

## Out of range

Reading or writing a position that does not exist is not checked in a normal
build. It will not stop the program with a helpful message; it will read or
write whatever happens to be next in memory. Two habits avoid it: use
`.size - 1` rather than a counted-by-eye number, and end loops with
`until!(i >= a.size)` rather than a literal.

## Printing one

`.str` gives the contents in braces, which is handy while working something
out:

```sather
   #OUT + shelf.str;      -- {Emma,Dracula,Kim}
```
