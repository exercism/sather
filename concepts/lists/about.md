# Lists

`LIST{T}` is a growable, ordered collection, backed by an array that is
replaced with a larger one when it fills up.

```sather
   notes ::= #LIST{STR};
   notes.append("muddy boots");
   notes[0]                     -- "muddy boots"
   notes[0] := "clean boots";
   notes.size
   notes.is_empty
   notes.has("clean boots")
   notes.remove_index(0);
```

## Array or list?

| | `ARRAY{T}` | `LIST{T}` |
| --- | --- | --- |
| size | fixed at creation | changes |
| append | no | yes |
| remove | no | yes |
| indexing | `a[i]` | `l[i]` |
| overhead | none | a size, and spare room |

Use an `ARRAY` when the size is known and settled — a row of dancers, a
week of counts. Use a `LIST` when things arrive or leave.

## In place, not functional

`append`, `remove_index` and `[i] :=` all change the list itself. Nothing
needs assigning back, and a list handed to a routine is not safe from it.

That is the opposite of `FMAP` and `FSET`, and it is worth being clear which
you are holding. The rule of thumb: `F` at the front of the name means
functional, and everything else changes in place.

To hand out a list nothing can spoil, give away a copy:

```sather
   return notes.copy;
```

## The cost of appending

Appending is cheap on average. When the backing array fills, a new one twice
the size is taken and everything is copied — so most appends cost nothing
much and occasional ones cost a copy. Over many appends that averages out to
a constant each, which is why the doubling is done rather than growing by
one each time.

`remove_index` is not cheap: everything after the removed position shifts up
by one. Removing repeatedly from the front of a long list is slow in a way
that is easy not to notice.

## Useful routines

| Call | Does |
| --- | --- |
| `l.append(x)` | adds to the end |
| `l.insert_before(i, x)` | adds at a position |
| `l.remove_index(i)` | takes a position out |
| `l.has(x)` | is it in there? |
| `l.copy` | an independent copy |
| `l.str` | the contents, in braces |
| `l.elt!`, `l.ind!` | walk the values, or the positions |
