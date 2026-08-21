# Abstract Classes

```sather
abstract class $ACT is
   name : STR;
   minutes : INT;
end;

class JUGGLING < $ACT is
   name : STR is return "Juggling"; end;
   minutes : INT is return 5; end;
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
class TRAPEZE < $ACT is
```

The class must define every routine listed, with matching argument types and
return type. It is checked when compiled.

A class may conform to several:

```sather
class TRAPEZE < $ACT, $RISKY is
```

and abstract classes may extend one another:

```sather
abstract class $TIMED_ACT < $ACT is
   overrun : INT;
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
   typecase act
   when TRAPEZE then #OUT + "rig the net";
   else            #OUT + "nothing to rig";
   end;
```

Inside an arm, the variable has the narrower type. Reach for it rarely: a
`typecase` over every kind of act is usually a routine that belonged in the
abstract class in the first place.

## $OB

`$OB` is the abstract class every object conforms to. It is occasionally
useful and mostly a sign that a type has been lost along the way.

## Why not inheritance?

Sather separates two things most languages join. `<` says only what a class
can *do*. Getting an implementation from somewhere else is `include`, which
is the next exercise but one, and is a separate decision.
