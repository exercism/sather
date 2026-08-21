# Generic Classes

```sather
class LOST_BOX{T} is
   attr item : T;
   create(thing : T) : SAME is
      box ::= new;
      box.item := thing;
      return box;
   end;
end;
```

## What the parameter is

`T` stands for a type supplied at the point of use. Sather builds a distinct
class for each combination actually used, when the program is compiled. So:

- `LOST_BOX{STR}` and `LOST_BOX{INT}` are unrelated types;
- there is no run-time check, no boxing and no conversion;
- an error in the class shows up for each type it is used with.

This is the same approach as C++ templates or Rust generics, and unlike Java
generics, where the type is erased and everything is really an object.

## Constrained parameters

A bare `T` can be assigned, passed and returned — nothing else, because
nothing else is known about it. To call routines on it, say what it must
conform to:

```sather
class LOST_BOX{T < $STR} is
   describe : STR is return "a box holding " + item.str; end;
end;
```

`T < $STR` demands that `T` conforms to `$STR`, and in return lets `item.str`
be called. Anything a bare `T` cannot do, a constraint is how to allow it.

Without the constraint, `item.str` will not compile — and the message will
name the line inside the generic class, not the line that used it.

## Generic routines?

There are none. Only classes take parameters. A routine that needs to work
over several types either lives in a generic class, or takes an abstract
type such as `$STR`.

## Choosing between them

| | generic class | abstract class |
| --- | --- | --- |
| decided | when compiled | when run |
| holds | one type per instantiation | any conforming type |
| cost | none | a dispatch |

`ARRAY{$ACT}` uses both: generic in the element type, abstract in what that
element can be.

Reach for a generic class when the type is the same throughout and the user
of the class knows it. Reach for an abstract class when several types must
coexist in one collection.
