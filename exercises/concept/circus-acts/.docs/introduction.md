# Abstract Classes

A bicycle shop sells unicycles, tricycles and road bikes. They are
different things with different insides, but the person writing the price
tags only needs two things from each: what it is called, and how many wheels
it has.

An **abstract class** describes that much and no more.

```sather
abstract class $CYCLE is
   model : STR;
   wheels : INT;
end; -- abstract class $CYCLE
```

Its name starts with `$`. It lists routines with no bodies: signatures only,
each ending at the semicolon. Nothing can be made from it — there is no
`create` and no `new`.

## Conforming

A real class promises to be a `$CYCLE` by naming it after `<`:

```sather
class UNICYCLE < $CYCLE is

   create : SAME is return new; end;

   model : STR is return "Unicycle"; end;

   wheels : INT is return 1; end;

end; -- class UNICYCLE
```

`<` is read "is a". The class must supply every routine the abstract class
lists, with the same arguments and the same return type. Leaving one out is
a compile error, not a surprise at run time.

A class may add whatever else it likes. `ROAD_BIKE` can hold a number of
gears that no other cycle has, and be made with `#ROAD_BIKE(21)`; the
abstract class neither knows nor cares.

## Using the type

`$CYCLE` is a type, so anything can be declared with it:

```sather
   stock : ARRAY{$CYCLE} := |#UNICYCLE, #ROAD_BIKE(21), #TRICYCLE|;
```

That array holds objects of three different classes at once, which an
`ARRAY{UNICYCLE}` could not.

## Dispatch

```sather
   loop
      cycle ::= stock.elt!;
      #OUT + cycle.model + ", wheels: " + cycle.wheels + "\n";
   end;
```

`cycle` is a `$CYCLE`. Which `wheels` runs is decided when the line runs,
by what the object actually is: `UNICYCLE::wheels` for the unicycle,
`ROAD_BIKE::wheels` for the road bike. That choosing is called
**dispatch**.

The loop writing the tags never asks what kind of cycle it has. Stocking a
fourth kind means writing one new class and changing nothing else — which
is the whole reason to do it this way.
