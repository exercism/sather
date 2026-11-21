# Lists

An `ARRAY` is fixed. It is made at one size and stays that size: there is no
appending to one, and no removing from one.

A kitchen shopping list is not like that. Things are added as the cook
notices they are running low, and crossed off once they are bought. For
that you want a **list**.

```sather
   shopping ::= #FLIST{STR};
   shopping := shopping.push("flour");
   shopping := shopping.push("eggs");
   shopping.size                -- 2
```

`FLIST{T}` holds values of type `T` in order, like an array, and grows and
shrinks as you ask it to.

## Always assign the answer back

`push` adds a value to the end, and answers the list to use from now on.
That answer has to be kept:

```sather
   shopping := shopping.push("flour");     -- yes
   shopping.push("flour");                 -- no: the answer is lost
```

Usually the answer is the very list that went in, changed in place. When the
list has run out of room, it is a new, larger one instead, with everything
copied across. You cannot tell which, so **use the answer and stop using the
old name.** A name left over from before a `push` may be out of date, or may
not describe a usable list at all.

That also means a list handed to a routine is not safe from it. If the
routine pushes, the routine's answer is the list to keep:

```sather
   shopping := add_essentials(shopping);
```

## An empty list is void

A list that has never had anything pushed onto it is **void**:
`#FLIST{STR}` makes no object at all. That is fine: pushing onto a void list
is how a list first comes into being, and `size`, `is_empty`, `elt!` and
`str` all cope with one.

```sather
   empty ::= #FLIST{STR};
   empty.size                   -- 0
   empty.is_empty               -- true
```

## Setting room aside

As with `FSTR`, a size can be given when the list is made:

```sather
   squares ::= #FLIST{INT}(100);
   squares.size                 -- 0
```

That sets aside room for a hundred values, so the first hundred pushes never
have to copy anything. It is worth doing when the size is known, or roughly
known. The list is still **empty**: its size is nought, and there is no
`squares[0]` until something has been pushed. This is the difference from
`#ARRAY{INT}(100)`, which makes a hundred positions ready to use.
`#FLIST{INT}(0)` is void, just like `#FLIST{INT}`.

## Reading and writing

Square brackets, counting from nought, exactly as for an array:

```sather
   shopping[0]                  -- "flour"
   shopping[1] := "duck eggs";
```

These need the position to be in the list, and so they do not work on a void
list at all. Check `size` before reaching for a position.

## Removing

`delete_ordered` takes a position out, and everything after it moves up one.
It answers the list to use from now on, just as `push` does:

```sather
   shopping := shopping.delete_ordered(0);    -- the flour is crossed off
```

So positions are not permanent. An item's position changes when an earlier
one is removed, which is worth remembering before storing one.

Beware the shorter `delete`. It is quicker because it moves the **last**
item into the gap, so the order is lost. Use `delete_ordered` unless the
order really does not matter.

## Walking it

`elt!` works, as it does on an array:

```sather
   loop
      #OUT + shopping.elt! + "\n";
   end;
```

## Making an array from it

A list is often built up a piece at a time and then handed on as an `ARRAY`.
`as_array` makes an array holding the list's values, in order:

```sather
   bought : ARRAY{STR} := shopping.as_array;
```

This is the usual way to finish: build with an `FLIST` inside a routine, and
hand back the settled `ARRAY`, the way an `FSTR` is built and its `.str`
handed back.

## The braces

`FLIST{STR}` is a list of strings, `FLIST{INT}` a list of numbers. It is a
generic class, exactly like the one you wrote in `lost-property` — and now
you can read the library's own the same way.
