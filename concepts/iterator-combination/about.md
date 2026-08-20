# Iterator Combination

Several iterators may share a loop. Each is advanced once per turn.

```sather
   loop
      a ::= xs.elt!;
      b ::= ys.elt!;
      ...
   end;
```

## Termination

The loop ends the moment **any** iterator has nothing left. The remaining
iterators are not advanced, and the rest of the body does not run.

That means walking two arrays together covers `min(xs.size, ys.size)`
turns. To cover the longer one, walk positions instead and index, guarding
the shorter array yourself.

## Each call site is its own walk

An iterator's position belongs to the *place in the program* where it is
written, not to the object. So:

```sather
   loop
      #OUT + xs.elt! + xs.elt!;      -- two walks, each advancing separately
   end;
```

takes two different elements per turn from two independent walks. Ask once
and keep the value.

## Endless iterators

| Iterator | Gives |
| --- | --- |
| `n.up!` | `n`, `n+1`, `n+2`, … for ever |
| `n.upto!(m)` | `n` … `m`, then ends |

An endless iterator must be paired with something that ends, or with
`break!` or `until!`. Alone it loops for ever.

Pairing `1.up!` with a walk over a collection is the idiomatic way to number
items, and is worth recognising on sight.

## Why this is one concept and not part of another

A loop that ends when its *first* iterator runs out is the single rule most
likely to produce a program that is quietly wrong rather than obviously
broken: it does not crash, it just stops early. Folding it into the exercise
that introduces iterators, or into the one that writes them, would mean
meeting it while something else is also new.
