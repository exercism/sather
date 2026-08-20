# Iterator Combination

A loop may call more than one iterator. Each is asked for its next value
once per turn, and they move forward together.

```sather
   loop
      first ::= violin_one.elt!;
      second ::= violin_two.elt!;
      #OUT + first + " against " + second + "\n";
   end;
```

That walks both arrays side by side: first element with first element,
second with second.

## The rule that surprises everybody

**The loop ends as soon as the *first* of its iterators runs out.**

Not when the last one does. Not when all of them have. The first.

So if `violin_one` holds four bars and `violin_two` holds two, the loop
above runs **twice**. The third and fourth bars of the first part are never
looked at, because by then the second part has nothing left to offer.

That is usually exactly what is wanted — pairing things up only makes sense
while there are pairs — but it has to be known rather than discovered.

## Counting alongside

An iterator that never runs out is useful precisely because of that rule.
`up!` counts forever:

```sather
1.up!        -- 1, 2, 3, 4, ... and never ends
```

On its own it would loop forever. Paired with one that does end, it numbers
the values without ever deciding how far to count:

```sather
   loop
      number ::= 1.up!;
      bar ::= part.elt!;
      #OUT + "Bar " + number + ": " + bar + "\n";
   end;
```

`part.elt!` ends the loop; `1.up!` supplies the numbering. Neither has to
know how long the part is.

## Order does not matter

The iterators are all asked once per turn, so it makes no difference which
is written first. What matters is that each is asked exactly once — writing
`part.elt!` twice in one turn takes two values instead of one.
