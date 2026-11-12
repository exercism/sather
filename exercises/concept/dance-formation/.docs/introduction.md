# Arrays

An **array** holds a row of values, all of the same type, in order.

The type is written `ARRAY{T}`, where `T` is what it holds. An array of
strings is `ARRAY{STR}`; an array of whole numbers is `ARRAY{INT}`.

```sather
   shelf : ARRAY{STR} := |"Emma", "Dracula", "Kim"|;
```

The values between the two `|` marks are the **array literal**. Sather works
out the size from how many there are.

## Getting a value out

Square brackets hold the position:

```sather
shelf[0]    -- "Emma"
shelf[1]    -- "Dracula"
shelf[2]    -- "Kim"
```

Counting starts at **nought**, not one. So the first value is at `0`, and
the last one in a row of three is at `2`.

## How many?

`.size` is how many values the array holds.

```sather
shelf.size  -- 3
```

Because counting starts at nought, the last position is always `.size - 1`:

```sather
shelf[shelf.size - 1]     -- "Kim"
```

Asking for a position that is not there — `shelf[3]`, or `shelf[-1]` — is a
mistake Sather will not catch for you, so it is worth writing `.size - 1`
rather than counting the values by eye.

## Walking through one

An array and a loop go together. Count a variable up through the positions
and use it to reach each value:

```sather
   i ::= 0;
   loop
      until!(i >= shelf.size);
      #OUT + "Shelved: " + shelf[i] + "\n";
      i := i + 1;
   end;
```

The test uses `shelf.size` rather than `3`, so the same loop works for a
shelf of any length, an empty one included.

## Arrays of arrays

The values in an array can themselves be arrays. A seating plan with a row
of dancers on each line is an `ARRAY{ARRAY{STR}}`: an array whose values
are each an `ARRAY{STR}`.

```sather
   seats : ARRAY{ARRAY{STR}} := | |"Lou", "Raj"|, |"Tess", "Kai", "Zoe"| |;
```

The inner literals sit inside the outer one, separated by commas. Leave a
space between neighbouring `|` marks, as in `| |"Lou"`, so they are not
read together.

One pair of square brackets picks a row; a second picks a value in that
row:

```sather
seats[1]          -- |"Tess", "Kai", "Zoe"|
seats[1][2]       -- "Zoe"
seats.size        -- 2, the number of rows
seats[1].size     -- 3, the number in that row
```

The rows need not all be the same length.

`#ARRAY{ARRAY{INT}}(3)` makes room for three rows, but each starts out
**void** — there is no row there yet. Make each one before using it:

```sather
   grid ::= #ARRAY{ARRAY{INT}}(3);
   grid[0] := #ARRAY{INT}(4);     -- row 0 is now four noughts
   grid[0][1] := 7;
```
