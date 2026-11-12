# Lists

An `ARRAY` is fixed. It is made at one size and stays that size: there is no
appending to one, and no removing from one.

A kitchen shopping list is not like that. Things are added as the cook
notices they are running low, and crossed off once they are bought. For
that you want a **list**.

```sather
   shopping ::= #LIST{STR};
   shopping.append("flour");
   shopping.append("eggs");
   shopping.size                -- 2
```

`LIST{T}` holds values of type `T` in order, like an array, and grows and
shrinks as you ask it to.

## It changes in place

`append` changes the list it is called on and answers nothing:

```sather
   shopping.append("flour");               -- yes
   shopping := shopping.append("flour");   -- no: append answers nothing
```

This is different from `FMAP` and `FSET`, where every change had to be
assigned back. A `LIST` is an ordinary object, like a `SCOREBOARD`: hand it
to a routine and the routine can change yours.

## Reading and writing

Square brackets, counting from nought, exactly as for an array:

```sather
   shopping[0]                  -- "flour"
   shopping[1] := "duck eggs";
   shopping.size                -- how many
   shopping.is_empty            -- true when there are none
```

## Removing

`remove_index` takes a position out, and everything after it moves up one:

```sather
   shopping.remove_index(0);    -- the flour is crossed off
```

So positions are not permanent. An item's position changes when an earlier
one is removed, which is worth remembering before storing one.

## Walking it

`elt!` works, as it does on an array:

```sather
   loop
      #OUT + shopping.elt! + "\n";
   end;
```

## The braces

`LIST{STR}` is a list of strings, `LIST{INT}` a list of numbers. It is a
generic class, exactly like the one you wrote in `lost-property` — and now
you can read the library's own the same way.
