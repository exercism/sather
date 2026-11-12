# Iterator Combination

A loop may call more than one iterator. Each is asked for its next value
once per turn, and they move forward together.

```sather
   loop
      fruit ::= fruits.elt!;
      price ::= prices.elt!;
      #OUT + fruit + ": " + price + "p\n";
   end;
```

That walks both arrays side by side: first element with first element,
second with second.

## The rule that surprises everybody

**The loop ends as soon as the *first* of its iterators runs out.**

Not when the last one does. Not when all of them have. The first.

So if `fruits` holds four fruits and `prices` holds two prices, the loop
above runs **twice**. The third and fourth fruits are never looked at,
because by then there is no price left to put beside them.

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
      stall ::= 1.up!;
      fruit ::= fruits.elt!;
      #OUT + "Stall " + stall + " sells " + fruit + "\n";
   end;
```

`fruits.elt!` ends the loop; `1.up!` supplies the numbering. Neither has to
know how many fruits there are.

## Order does not matter

The iterators are all asked once per turn, so it makes no difference which
is written first. What matters is that each is asked exactly once — writing
`fruits.elt!` twice in one turn takes two values instead of one.
