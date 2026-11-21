# Maps and Sets

| Type | Holds | Look up by |
| --- | --- | --- |
| `ARRAY{T}` | values in order | position |
| `FMAP{K,T}` | key-target pairs | key |
| `FSET{T}` | values, no repeats | membership |

## FMAP

```sather
   m ::= #FMAP{STR,INT};
   m := m.insert("hammer", 12);
   m.get("hammer")       -- 12
   m.has_ind("hammer")   -- true
   m.size                -- 1
   m := m.delete("hammer");
```

`m["hammer"]` is **not** how to read a map — `FMAP` has no such routine, and
that line will not compile. It is `get`.

### Missing keys

`get` on a key that is not there answers the empty value for the type rather
than complaining: `0`, `false`, or void. A void `STR` will not fail where it
is produced; it fails later, wherever it is finally used. `has_ind` first is
the habit worth forming.

## FSET

```sather
   s ::= #FSET{STR};
   s := s.insert("paint");
   s.has("paint")        -- true
   s.size                -- 1
   s := s.delete("paint");
```

Sets combine:

```sather
   a.union(b)            -- in either
   a.intersect(b)        -- in both
   a.difference(b)       -- in a but not b
   a.is_subset(b)
```

## Assigning back, and copying

`insert` and `delete` answer the container to use from now on. Usually that
is the same object, changed in place; when it has to grow, it is a new,
larger one. So:

```sather
   m := m.insert(k, v);     -- always
```

and the name on the left is the only one to trust afterwards. Another name
for the same map, taken before the `insert`, may be stale.

To keep an independent copy, take one first:

```sather
   n ::= m.copy.insert(k, v);      -- m is unchanged
```

with one catch: a map that has never had anything inserted is **void**, and
`copy` on a void map fails. `insert`, `get`, `has_ind` and `size` all cope
with a void map — `#FMAP{K,T}` is void, and inserting into it is how a map
first comes into being — but `copy` does not.

`HMAP` and `HSET` are the versions that only ever change in place. They are
faster for building something large, and they are the wrong default while
learning.

## Walking one

| Iterator | Gives |
| --- | --- |
| `m.ind!` | each key |
| `m.target!` | each target |
| `m.pair!` | each key and target together |
| `s.elt!` | each value of a set |

Neither a map nor a set has an order. Two runs may walk them differently, so
never write anything that depends on which comes first. Don't insert into or
delete from a map or set while walking it.

```sather
   loop
      #OUT + stock.ind! + "\n";
   end;
```

## Keys and targets together

`pair!` gives each key with its target, packed into a **tuple**: a
`TUP{K,T}`, a small immutable object holding the two values. `.t1` is the
key and `.t2` the target.

```sather
   loop
      p ::= stock.pair!;
      #OUT + p.t1 + ": " + p.t2 + "\n";
   end;
```

That saves walking the keys and looking each one up again with `get`. The
type can be written out in full when it helps:

```sather
      p : TUP{STR,INT} := stock.pair!;
```

As with anything from a map, the pairs come in no particular order.

Tuples come in other sizes too, and one can be made directly. The types
have to be given:

```sather
   t ::= #TUP{STR,INT,BOOL}("saw", 3, true);
   t.t3                         -- true
```

A bare `#TUP("saw", 3, true)` does not compile.
