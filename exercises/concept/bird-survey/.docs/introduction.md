# Iterators

Walking an array with a counter takes four lines of bookkeeping before any
work happens:

```sather
   i ::= 0;
   loop
      until!(i >= counts.size);
      total := total + counts[i];
      i := i + 1;
   end;
```

The counter, the ending test and the step have nothing to do with adding
numbers up. An **iterator** does all three.

```sather
   loop
      total := total + counts.elt!;
   end;
```

`elt!` hands over one element each time round, and ends the loop when there
are no more. No counter, nothing to get wrong, and no way to run off the
end of the array.

## The exclamation mark

The `!` marks an iterator. You have met three already — `until!`, `while!`
and `break!` — and they follow the same rule: **an iterator may only be
called inside a loop.** Writing `counts.elt!` outside one is an error.

An iterator called inside a loop is asked for a value each time round. When
it has none left, the loop ends immediately, wherever in the body the call
happens to be.

## Two to start with

`elt!` gives the elements of an array or a string, in order.

```sather
   loop
      #OUT + names.elt! + "\n";
   end;
```

`upto!` counts. `1.upto!(5)` gives 1, 2, 3, 4, 5 and then ends the loop.

```sather
   loop
      total := total + 1.upto!(5);
   end;
```

Both are ordinary routines that happen to end in `!`, so both are called
with a dot, on an array or on a number.

## Keeping the answer

The loop ends by itself, so anything worked out inside it has to be kept in
a variable declared **outside** — otherwise it disappears when the loop
does.

```sather
   total ::= 0;             -- outside
   loop
      total := total + counts.elt!;
   end;
   return total;
```
