# Immutable Classes

```sather
immutable class LEG is
   readonly attr origin, destination : STR;
   create(from, to : STR) : SAME is
      leg : SAME;
      return leg.origin(from).destination(to);
   end;
end;
```

## What changes

| | ordinary class | immutable class |
| --- | --- | --- |
| assignment | shares the object | copies the value |
| can be void | yes | no |
| `attr` writer | `x.a := v` | `x := x.a(v)` |
| `new` | yes | no; `x : SAME` already exists |

An immutable object cannot be void, so `void(leg)` is always false and no
routine on one can fail for want of an object. That removes a whole class of
mistake at the cost of never being able to say "no leg yet".

## Where the value lives

The value is stored where the variable is — inside another object, or on the
stack — rather than being reached through a reference. So an
`ARRAY{LEG}` holds the legs themselves, not pointers to them, which
is smaller and faster to walk.

The cost is copying: passing a large immutable object copies it every time.
They are best kept small.

## The attribute routines

`readonly attr origin : STR` gives two routines:

```sather
   leg.origin            -- read: STR
   leg.origin("Leeds")   -- answer a new LEG with origin changed
```

The second exists even under `readonly`, because it changes nothing — it
builds a new value. Under a plain `attr` it is public; under `private attr`
it is not.

## is_eq and str

Neither is provided. Write `is_eq` for `=`, and `str` so the object can be
printed and joined to strings:

```sather
   is_eq(leg : SAME) : BOOL is
      return origin = leg.origin and destination = leg.destination;
   end;
   str : STR is return origin + " to " + destination; end;
```

Writing `str` is not enough on its own for `+` and `#OUT` to accept the
object: they take a `$STR`, so the class must also say it is one, with
`immutable class LEG < $STR is`.

## The built-in ones

`INT`, `BOOL`, `CHAR`, `FLTD` and `TUP` are all immutable classes. Nothing
about them is special: they are written in Sather in the library the same
way, and behave the way they do for the reasons above.
