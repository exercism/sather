# Bound Routines

```sather
   part : ROUT{STR}:STR := bind(shout(_));
   part.call("who's there");
```

## bind

`bind` takes a call in which any part may be replaced by `_`. Everything not
a `_` is evaluated **now** and kept; every `_` becomes an argument of the
bound routine, in the order written.

```sather
   bind(repeat(2, _))         -- ROUT{STR}:STR
   bind(repeat(_, "Ha"))      -- ROUT{INT}:STR
   bind(repeat(_, _))         -- ROUT{INT,STR}:STR
```

## The types

| Type | Takes | Answers |
| --- | --- | --- |
| `ROUT:INT` | nothing | `INT` |
| `ROUT{STR}` | a `STR` | nothing |
| `ROUT{STR}:STR` | a `STR` | a `STR` |
| `ROUT{INT,INT}:BOOL` | two `INT`s | `BOOL` |

`ITER{...}` is the same idea for an iterator.

## call

`call` supplies the remaining arguments. A bound routine answering nothing
is called the same way, as a statement.

## bind goes on the right of an assignment

A `bind` may be declared into a variable, or passed as an argument:

```sather
   part ::= bind(shout(_));                -- yes
   part : ROUT{STR}:STR := bind(shout(_)); -- yes
   rehearse("line", bind(shout(_)));       -- yes
```

but it may not go straight into a `return`:

```sather
   return bind(shout(_));                  -- does not parse
```

Put it in a variable and return that. The error message points at the
`bind` and mentions underscores, which is not obvious from the line itself.

## Where they are used

The library takes them wherever behaviour has to be supplied:

```sather
   names.sort_by(bind(shorter(_, _)));
   scores.count_if(bind(over(10, _)));
   scores.find_if(bind(is_even(_)));
```

Sorting is the clearest case: `sort_by` knows how to sort and nothing about
your idea of order, and the bound routine is how the two meet.

## A limitation in this compiler

Sather 1.2 does not implement **dispatched** bound routines — binding a
routine on a variable of an abstract type. The compiler says so plainly:

```
Dispatched bound routines are not implemented yet
```

Bind on a concrete type, or on a class, and all is well. This is why the
track's own test harness writes its exception checks out by hand rather than
taking a bound routine.

## Bound routines or abstract classes?

Both let a caller supply behaviour.

A bound routine is one routine, needs no class, and is written where it is
used. An abstract class carries several routines and some state, and is
worth the ceremony when the thing supplied has more than one part to it.

One routine to hand over: bind it. A collaborator with several: write a
class.
