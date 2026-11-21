# Lists

`FLIST{T}` is a growable, ordered collection, backed by an array that is
replaced with a larger one when it fills up.

```sather
   pantry ::= #FLIST{STR};
   pantry := pantry.push("rice");
   pantry[0]                    -- "rice"
   pantry[0] := "brown rice";
   pantry.size
   pantry.is_empty
   pantry.has("brown rice")
   pantry := pantry.delete_ordered(0);
```

## Array or list?

| | `ARRAY{T}` | `FLIST{T}` |
| --- | --- | --- |
| size | fixed at creation | changes |
| add to the end | no | `l := l.push(x)` |
| remove | no | `l := l.delete_ordered(i)` |
| indexing | `a[i]` | `l[i]` |
| empty | an array of size 0 | void |
| overhead | none | a size, and spare room |

Use an `ARRAY` when the size is known and settled — the days of a
week, the squares of a board. Use an `FLIST` when things arrive or leave.

A common shape is both: an `FLIST` inside a routine while the answer is being
gathered, and `as_array` at the end to hand back an `ARRAY`.

```sather
   evens(upto : INT) : ARRAY{INT} is
      found ::= #FLIST{INT};
      loop
         n ::= 0.upto!(upto);
         if n % 2 = 0 then found := found.push(n) end;
      end;
      return found.as_array;
   end;
```

## Assigning back, and copying

`push`, `delete_ordered`, `insert_before` and `insert_after` answer the list
to use from now on. Usually that is the same object, changed in place; when
it has to grow, it is a new, larger one, and the old one is destroyed. So:

```sather
   l := l.push(x);     -- always
```

and the name on the left is the only one to trust afterwards. Another name
for the same list, taken before the `push`, may be stale.

To keep an independent copy, take one first:

```sather
   m ::= l.copy.push(x);      -- l is unchanged
```

A list that has never had anything pushed onto it is **void**. `#FLIST{T}`
is void, and pushing onto it is how a list first comes into being. `push`,
`size`, `is_empty`, `has`, `elt!`, `str`, `copy` and `as_array` all cope with
a void list; `l[i]` and `delete_ordered` need a position that exists, so
they do not.

The rule of thumb: `F` at the front of the name means "assign the answer
back". `LIST{T}` is the version that only ever changes in place: its
`append` answers nothing. It is the wrong default while learning, because it
cannot be told apart from an `FLIST` at a glance and the habits do not mix.

## Ordered and unordered deletion

`delete_ordered(i)` closes the gap by moving everything after `i` up one.
`delete(i)` instead moves the last item into position `i`: quicker, but the
order is lost. Pick `delete` only when the list is really a bag.

## The cost of appending

Pushing is cheap on average. When the backing array fills, a new one twice
the size is taken and everything is copied — so most pushes cost nothing
much and occasional ones cost a copy. Over many pushes that averages out to
a constant each, which is why the doubling is done rather than growing by
one each time.

When the number of values is known in advance, `#FLIST{T}(n)` sets aside
room for `n` of them, and those pushes never copy at all. The list still
starts empty — `size` is nought — unlike `#ARRAY{T}(n)`, which has `n`
positions ready. `#FLIST{T}(0)` is void.

`delete_ordered` is not cheap: everything after the removed position shifts
up by one. Removing repeatedly from the front of a long list is slow in a way
that is easy not to notice.

## Useful routines

| Call | Does |
| --- | --- |
| `#FLIST{T}(n)` | an empty list with room for `n` |
| `l := l.push(x)` | adds to the end |
| `l := l.insert_before(i, x)` | adds at a position |
| `l := l.delete_ordered(i)` | takes a position out, keeping the order |
| `l.has(x)` | is it in there? |
| `l.index_of(x)` | where is it? -1 if nowhere |
| `l.copy` | an independent copy |
| `l.as_array` | an `ARRAY` of the values, in order |
| `l.to_reverse` | reverses the list in place |
| `l.str` | the contents, in braces |
| `l.elt!`, `l.ind!` | walk the values, or the positions |
