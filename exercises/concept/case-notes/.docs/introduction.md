# Lists

An `ARRAY` is fixed. It is made at one size and stays that size: there is no
appending to one, and no removing from one.

A detective's notebook is not like that. Clues turn up one at a time, and
get struck out when they are ruled out. For that you want a **list**.

```sather
   notes ::= #LIST{STR};
   notes.append("muddy boots");
   notes.append("broken window");
   notes.size                   -- 2
```

`LIST{T}` holds values of type `T` in order, like an array, and grows and
shrinks as you ask it to.

## It changes in place

`append` changes the list it is called on and answers nothing:

```sather
   notes.append("muddy boots");        -- yes
   notes := notes.append("muddy boots");   -- no: append answers nothing
```

This is different from `FMAP` and `FSET`, where every change had to be
assigned back. A `LIST` is an ordinary object, like a `SCOREBOARD`: hand it
to a routine and the routine can change yours.

## Reading and writing

Square brackets, counting from nought, exactly as for an array:

```sather
   notes[0]                     -- "muddy boots"
   notes[1] := "smashed window";
   notes.size                   -- how many
   notes.is_empty               -- true when there are none
```

## Removing

`remove_index` takes a position out, and everything after it moves up one:

```sather
   notes.remove_index(0);       -- the first clue is struck out
```

So positions are not permanent. A clue's position changes when an earlier
one is removed, which is worth remembering before storing one.

## Walking it

`elt!` works, as it does on an array:

```sather
   loop
      #OUT + notes.elt! + "\n";
   end;
```

## The braces

`LIST{STR}` is a list of strings, `LIST{INT}` a list of numbers. It is a
generic class, exactly like the one you wrote in `lost-property` — and now
you can read the library's own the same way.
