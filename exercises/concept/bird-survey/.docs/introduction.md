# Iterators

Walking an array with a counter takes four lines of bookkeeping before any
work happens:

```sather
   i ::= 0;
   loop
      until!(i >= crops.size);
      #OUT + "Sow " + crops[i] + "\n";
      i := i + 1;
   end;
```

The counter, the ending test and the step have nothing to do with sowing
seeds. An **iterator** does all three.

```sather
   loop
      crop ::= crops.elt!;
      #OUT + "Sow " + crop + "\n";
   end;
```

`elt!` hands over one element each time round, and ends the loop when there
are no more. No counter, and no way to run off the end of the array.

## Ask the iterator first

When an iterator runs out, the loop ends right there, in the middle of the
line that called it. Whatever that line had already done stays done. Sather
works along a line from left to right, so in

```sather
   -- don't
   loop
      #OUT + "Sow " + crops.elt! + "\n";
   end;
```

`"Sow "` has already been printed when `elt!` finds nothing left, and the
output ends with a stray `Sow `. Take the value into a variable on a line of
its own, as above, and then use it. Nothing has happened yet when that line
ends the loop.

## The exclamation mark

The `!` marks an iterator. You have met three already — `until!`, `while!`
and `break!` — and they follow the same rule: **an iterator may only be
called inside a loop.** Writing `crops.elt!` outside one is an error.

An iterator called inside a loop is asked for a value each time round. When
it has none left, the loop ends immediately, wherever in the body the call
happens to be.

## Three to start with

`elt!` gives the elements of an array or a string, in order.

```sather
   loop
      #OUT + crops.elt! + "\n";
   end;
```

The elements of a string are its characters, so on a string `elt!` gives
one `CHAR` each time round:

```sather
   loop
      letter ::= "leeks".elt!;      -- 'l', 'e', 'e', 'k', 's'
      #OUT + letter.upper + "\n";
   end;
```

`upto!` counts. `1.upto!(3)` gives 1, 2, 3 and then ends the loop.

```sather
   loop
      bed ::= 1.upto!(3);
      #OUT + "Water bed " + bed + "\n";
   end;
```

Counting from `0` to `.size - 1` gives the positions of an array, for when
the position matters as well as the value:

```sather
   loop
      i ::= 0.upto!(crops.size - 1);
      #OUT + "Bed " + i + ": " + crops[i] + "\n";
   end;
```

`downto!` counts the other way. `3.downto!(1)` gives 3, 2, 1. Counting
down from `.size - 1` to `0` visits the positions last first, which is the
quick way to find the *last* of something: stop at the first one found
going backwards.

```sather
   loop
      i ::= (crops.size - 1).downto!(0);
      #OUT + "Bed " + i + ": " + crops[i] + "\n";
   end;
```

The brackets matter. Without them, `crops.size - 1.downto!(0)` counts down
from `1`, not from the last position, because the call happens before the
subtraction.

All three are ordinary routines that happen to end in `!`, so all are called
with a dot, on an array or on a number.

## Keeping the answer

The loop ends by itself, so anything worked out inside it has to be kept in
a variable declared **outside** — otherwise it disappears when the loop
does.

```sather
   has_leeks ::= false;           -- outside
   loop
      if crops.elt! = "leeks" then has_leeks := true; end;
   end;
   return has_leeks;
```

## Splitting a string

`(s + c).split!(c)` gives the pieces of the string `s` separated by the
character `c`, with every piece ending in `c`:

```sather
   ("who am i" + ' ').split!(' ')      -- "who ", "am ", "i "
   ("who am i " + ' ').split!(' ')     -- "who ", "am ", "i "
```

Drop the last character of each piece to get the words on their own:

```sather
   loop
      piece ::= (phrase + ' ').split!(' ');
      word ::= piece.head(piece.size - 1);
      #OUT + "[" + word + "]\n";
   end;
```
