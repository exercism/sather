# About

Sather is an object-oriented language designed at the International Computer Science Institute (ICSI) in Berkeley from 1990.
It aims to be as efficient as C while staying safe, simple and readable.
GNU Sather, the implementation this track uses, compiles Sather to C.

A few ideas make Sather stand out:

- **Iters.**
  Loops are driven by iterators, routines whose names end in `!`.
  An iter `yield`s values back into the loop that calls it and carries on from there when the loop asks for the next one.
  The library supplies many, such as `elt!` and `times!`, and you can write your own.
- **Subtyping is separate from code reuse.**
  Abstract types such as `$SHAPE` say which classes can be used where.
  Reusing code is a different step: a class `include`s another class's code, and can rename or leave out parts of it.
- **Design by contract.**
  Routines can state `pre` and `post` conditions, and classes can state an `invariant`.
  The compiler can check them all as the program runs.
- **Reference and immutable classes.**
  Most objects are references, but `immutable class`es behave like values, the way numbers do.
- **Strong, static typing.**
  There are no implicit conversions, and every routine call is checked when the program compiles.

Here is an iter that yields the first `n` Fibonacci numbers:

```sather
fib!(n : INT) : INT is
   a ::= 0; b ::= 1;
   loop n.times!;
      yield a;
      t ::= a + b; a := b; b := t
   end
end;
```

`loop #OUT + fib!(10).str + " " end` prints `0 1 1 2 3 5 8 13 21 34`.
