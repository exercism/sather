# Code Inclusion

```sather
   include WARM_UP;
   include WARM_UP count -> warm_up_count;
   include WARM_UP describe -> ;
   include WARM_UP count -> beats, describe -> ;
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

Renaming applies to what the *outside* sees. Calls between the included
routines still work: if `describe` calls `count` and `count` is renamed to
`beats`, `describe` calls `beats`.

## Including several

```sather
   include WARM_UP;
   include COOL_DOWN;
```

is allowed, and is how Sather gets what other languages call multiple
inheritance — without the usual trouble, because a clash is a compile error
and the fix is to rename or leave one out. Nothing is resolved by an order
of precedence you have to memorise.

## private include

```sather
   private include WARM_UP;
```

brings the code in for this class's own use without exposing it. Useful when
you want the implementation and not the interface.

## The two together

The usual shape for a family of classes:

```sather
abstract class $ACT is
   name : STR;
   minutes : INT;
end;

class ACT_BASICS is
   minutes : INT is return 5; end;
end;

class JUGGLING < $ACT is
   include ACT_BASICS;
   name : STR is return "Juggling"; end;
end;
```

`< $ACT` says what it can do; `include ACT_BASICS` supplies part of the how.
Change your mind about the how and the `<` does not move.

## Why it is done this way

An abstract class has no code, so it cannot be inherited from by accident,
and there is no such thing as a superclass whose behaviour changes under
you. Reuse is a copy taken at compile time, from a class you named, with
every renaming written down.

The cost is that reuse must be asked for explicitly in each class. That is
the trade: more to type, nothing implicit.
