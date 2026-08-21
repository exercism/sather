# Maps and Sets

An array holds values in numbered positions. Sometimes the useful label is
not a number.

## Maps

A **map** pairs each **key** with a **target**. Look something up by its key
and the map gives you what was filed under it.

`FMAP{K,T}` is a map from keys of type `K` to targets of type `T`. A guide
pairing an animal's name with where it lives is `FMAP{STR,STR}`.

```sather
   guide ::= #FMAP{STR,STR};
   guide := guide.insert("emu", "grassland");
   guide.get("emu")               -- "grassland"
```

## Always assign the answer back

Look again at that middle line. `insert` answers the map with the extra pair
in it, and the answer has to be kept:

```sather
   guide := guide.insert("emu", "grassland");     -- yes
   guide.insert("emu", "grassland");              -- no: the answer is lost
```

This is the same rule as `FSTR`, and for the same reason. The answer is
usually the very map that went in, changed in place; occasionally, when the
map has run out of room, it is a larger one. Since you cannot tell which,
**use the answer and stop using the old name.** A name left over from before
an `insert` may be out of date or may not describe a usable map at all.

That also means a map handed to a routine is not safe from it. If the
original has to survive, see `copy` on the concept page.

## Is it there?

`has_ind` asks whether a key is in the map. The name is short for "has
index", an index being what these maps call a key.

```sather
   guide.has_ind("emu")           -- true
   guide.has_ind("moa")           -- false
```

Asking for a key that is not there does **not** complain. `get` hands back
the empty value for the type — nought for an `INT`, and void for a `STR`,
which will go wrong later and somewhere else. So look before you fetch:

```sather
   if guide.has_ind(animal) then
      return guide.get(animal);
   else
      return "Unknown";
   end;
```

## Sets

A **set** holds values with no repeats and no order. `FSET{T}` is a set of
values of type `T`.

```sather
   seen ::= #FSET{STR};
   seen := seen.insert("emu");
   seen := seen.insert("emu");    -- already there; nothing changes
   seen.size                      -- 1
   seen.has("emu")                -- true
```

Inserting something twice leaves one copy. That is what a set is for:
collecting things while forgetting how often each turned up.

`insert` on a set answers the set to use from then on, exactly as it does
for a map, so assign it back every time.

## How many

`.size` works on both: how many pairs a map holds, and how many values are
in a set.
