# Abstract Classes

```sather
abstract class $CYCLE is
   model : STR;
   wheels : INT;
end;

class TRICYCLE < $CYCLE is
   model : STR is return "Tricycle"; end;
   wheels : INT is return 3; end;
   create : SAME is return new; end;
end;
```

## The $ is part of the name

Every abstract class is named with a leading `$`, and only abstract classes
are. So a type beginning with `$` is one you cannot make an object of, and
that is visible everywhere the name appears.

## What may go in one

Routine and iterator signatures, ending at the semicolon. No bodies, no
attributes, no `create`. An abstract class describes what can be *asked* of
something, never what it holds.

## Conformance

```sather
class ROAD_BIKE < $CYCLE is
```

The class must define every routine listed, with matching argument types and
return type. It is checked when compiled.

A class may conform to several:

```sather
class ROAD_BIKE < $CYCLE, $FOR_HIRE is
```

and abstract classes may extend one another:

```sather
abstract class $GEARED_CYCLE < $CYCLE is
   gears : INT;
end;
```

## Where dispatch happens

A variable of an abstract type holds a reference to some conforming object.
Calling a routine on it picks the version belonging to the object's real
class, at run time.

That is the one place Sather decides anything at run time. A call on a
variable of a concrete type is settled when compiled.

## typecase

Sometimes the kind really does matter. `typecase` asks:

```sather
   typecase cycle
   when ROAD_BIKE then #OUT + "oil the gears";
   else              #OUT + "no gears to oil";
   end;
```

Inside an arm, the variable has the narrower type. Reach for it rarely: a
`typecase` over every kind of cycle is usually a routine that belonged in the
abstract class in the first place.

## $OB

`$OB` is the abstract class every object conforms to. It is occasionally
useful and mostly a sign that a type has been lost along the way.

## Why not inheritance?

Sather separates two things most languages join. `<` says only what a class
can *do*. Getting an implementation from somewhere else is `include`, which
is the next exercise but one, and is a separate decision.
