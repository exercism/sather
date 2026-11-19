# Generic Classes

```sather
class PAIR{T} is
   attr left, right : T;
   create(a, b : T) : SAME is
      pair ::= new;
      pair.left := a;
      pair.right := b;
      return pair;
   end;
end;
```

## What the parameter is

`T` stands for a type supplied at the point of use. Sather builds a distinct
class for each combination actually used, when the program is compiled. So:

- `PAIR{STR}` and `PAIR{INT}` are unrelated types;
- there is no run-time check, no boxing and no conversion;
- an error in the class shows up for each type it is used with.

This is the same approach as C++ templates or Rust generics, and unlike Java
generics, where the type is erased and everything is really an object.

## Constrained parameters

A class that calls a routine on a `T` works only for types that have that
routine. A constraint states that requirement in the header:

```sather
class PAIR{T < $STR} is
   label : STR is return "Pair: " + left.str + " & " + right.str; end;
end;
```

`T < $STR` says that `T` must conform to `$STR`, so a reader learns from the
header alone what the class needs from its parameter.

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
