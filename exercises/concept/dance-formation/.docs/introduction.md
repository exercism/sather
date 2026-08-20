# Arrays

An **array** holds a row of values, all of the same type, in order.

The type is written `ARRAY{T}`, where `T` is what it holds. An array of
strings is `ARRAY{STR}`; an array of whole numbers is `ARRAY{INT}`.

```sather
   row : ARRAY{STR} := |"Mia", "Ana", "Ben"|;
```

The values between the two `|` marks are the **array literal**. Sather works
out the size from how many there are.

## Getting a value out

Square brackets hold the position:

```sather
row[0]      -- "Mia"
row[1]      -- "Ana"
row[2]      -- "Ben"
```

Counting starts at **nought**, not one. So the first value is at `0`, and
the last one in a row of three is at `2`.

## How many?

`.size` is how many values the array holds.

```sather
row.size    -- 3
```

Because counting starts at nought, the last position is always `.size - 1`:

```sather
row[row.size - 1]     -- "Ben"
```

Asking for a position that is not there — `row[3]`, or `row[-1]` — is a
mistake Sather will not catch for you, so it is worth writing `.size - 1`
rather than counting the values by eye.

## Walking through one

An array and a loop go together. Count a variable up through the positions
and use it to reach each value:

```sather
   total ::= 0;
   i ::= 0;
   loop
      until!(i >= scores.size);
      total := total + scores[i];
      i := i + 1;
   end;
```
