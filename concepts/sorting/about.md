# Sorting

```sather
   numbers.sort;                                  -- the natural order
   words.insertion_sort_by(bind(before(_, _)));   -- an order you supply
```

## What sort needs

`sort` requires the element type to have `is_lt`. `INT`, `STR`, `CHAR`,
`FLTD` and `INTI` all do. A class of your own does not until you write one.

`insertion_sort_by` requires nothing of the element type: everything it
needs to know is in the routine you hand it.

## What a comparison must be

The routine must define a consistent order, or the result is not defined:

- if `before(a, b)` is true then `before(b, a)` must be false;
- if `a` comes before `b` and `b` before `c`, then `a` before `c`;
- `before(a, a)` must be false.

The last is the one people trip over. Writing `<=` instead of `<` says a
thing comes before itself, and a sort given that can produce anything.

## Ties

Neither `sort` nor `insertion_sort_by` is **stable**: things the comparison
calls equal may come out in either order, and in this library they generally
come out reversed.

So the trick of sorting twice — once by name, then by points, expecting
teams level on points to stay alphabetical — does not work here. Nor does
relying on the input order for anything.

If ties matter, settle them **in the comparison**. Make it a total order,
so that no two different things are ever called equal:

```sather
   shorter(a, b : STR) : BOOL is
      if a.size /= b.size then return a.size < b.size; end;
      return a < b;                  -- same length: alphabetical
   end;
```

That is worth doing even when you think ties cannot happen. A comparison
that answers false both ways round leaves the result unspecified, and the
bug shows up as an order that changes for no visible reason.

## The others

| Call | Does |
| --- | --- |
| `a.sort` | in place, natural order, not stable |
| `a.insertion_sort_by(lt)` | in place, your order, stable |
| `a.is_sorted` | check |
| `a.is_sorted_by(lt)` | check against your order |
| `a.binary_search(e)` | find, on a sorted array |
| `a.binary_search_by(e, lt)` | find, against your order |

`binary_search` on an unsorted array does not fail — it answers nonsense.
Its precondition says as much, and preconditions are unchecked unless the
compiler is given `-chk`.

## Cost

Insertion sort does work proportional to the square of the length, which is
fine for a ladder of a dozen teams and wrong for ten thousand records.
`ARR_SORT_ALG::sort_by` is the quicksort version of the same idea, for when
the array is big and stability does not matter.
