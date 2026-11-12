# Code Inclusion

```sather
   include ROBOT_BASE;
   include ROBOT_BASE wheels -> base_wheels;
   include ROBOT_BASE blurb -> ;
   include ROBOT_BASE wheels -> base_wheels, blurb -> base_blurb;
```

An `include` copies the code of another class into this one. It is a
compile-time operation with no run-time cost and no run-time relationship:
the two classes are not connected afterwards.

## The clause

```
   include CLASS  old_name -> new_name , old_name -> ;
```

Each entry renames one feature. `-> ;` with no new name leaves it out.
Anything not mentioned comes in unchanged.

Calls inside the included code are looked up by name in the new class,
after the renaming. If `blurb` calls `wheels` and `wheels` is renamed to
`base_wheels`, the copied `blurb` still calls `wheels`: whatever this
class now has under that name. If it has nothing by that name, the compiler
refuses.

## Including several

```sather
   include ROBOT_BASE;
   include BATTERY;
```

is allowed, and is how Sather gets what other languages call multiple
inheritance — without the usual trouble, because a clash is a compile error
and the fix is to rename or leave one out. Nothing is resolved by an order
of precedence you have to memorise.

## private include

```sather
   private include ROBOT_BASE;
```

brings the code in for this class's own use without exposing it. Useful when
you want the implementation and not the interface.

## The two together

The usual shape for a family of classes:

```sather
abstract class $ROBOT is
   name : STR;
   wheels : INT;
end;

class ROBOT_PARTS is
   wheels : INT is return 4; end;
end;

class SWEEPER < $ROBOT is
   include ROBOT_PARTS;
   name : STR is return "Sweeper"; end;
end;
```

`< $ROBOT` says what it can do; `include ROBOT_PARTS` supplies part of the
how.
Change your mind about the how and the `<` does not move.

## Why it is done this way

An abstract class has no code, so it cannot be inherited from by accident,
and there is no such thing as a superclass whose behaviour changes under
you. Reuse is a copy taken at compile time, from a class you named, with
every renaming written down.

The cost is that reuse must be asked for explicitly in each class. That is
the trade: more to type, nothing implicit.
