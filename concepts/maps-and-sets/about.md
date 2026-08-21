# Maps and Sets

| Type | Holds | Look up by |
| --- | --- | --- |
| `ARRAY{T}` | values in order | position |
| `FMAP{K,T}` | key-target pairs | key |
| `FSET{T}` | values, no repeats | membership |

## FMAP

```sather
   m ::= #FMAP{STR,INT};
   m := m.insert("emu", 2);
   m.get("emu")          -- 2
   m.has_ind("emu")      -- true
   m.size                -- 1
   m := m.delete("emu");
```

`m["emu"]` is **not** how to read a map — `FMAP` has no such routine, and
that line will not compile. It is `get`.

### Missing keys

`get` on a key that is not there answers the empty value for the type rather
than complaining: `0`, `false`, or void. A void `STR` will not fail where it
is produced; it fails later, wherever it is finally used. `has_ind` first is
the habit worth forming.

## FSET

```sather
   s ::= #FSET{STR};
   s := s.insert("emu");
   s.has("emu")          -- true
   s.size                -- 1
   s := s.delete("emu");
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
never write anything that depends on which comes first.

```sather
   loop
      #OUT + guide.ind! + "\n";
   end;
```
