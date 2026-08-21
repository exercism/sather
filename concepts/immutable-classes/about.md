# Immutable Classes

```sather
immutable class BEARING is
   readonly attr degrees : INT;
   create(d : INT) : SAME is
      b : SAME;
      return b.degrees(d);
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

An immutable object cannot be void, so `void(b)` is always false and no
routine on one can fail for want of an object. That removes a whole class of
mistake at the cost of never being able to say "no bearing yet".

## Where the value lives

The value is stored where the variable is — inside another object, or on the
stack — rather than being reached through a reference. So an
`ARRAY{BEARING}` holds the bearings themselves, not pointers to them, which
is smaller and faster to walk.

The cost is copying: passing a large immutable object copies it every time.
They are best kept small.

## The attribute routines

`readonly attr degrees : INT` gives two routines:

```sather
   b.degrees          -- read: INT
   b.degrees(90)      -- answer a new BEARING with degrees changed
```

The second exists even under `readonly`, because it changes nothing — it
builds a new value. Under a plain `attr` it is public; under `private attr`
it is not.

## is_eq and str

Neither is provided. Write `is_eq` for `=`, and `str` so the object can be
printed and joined to strings:

```sather
   is_eq(other : SAME) : BOOL is return degrees = other.degrees; end;
   str : STR is return degrees.str + " degrees"; end;
```

Writing `str` makes the class conform to `$STR`, which is what lets `+` and
`#OUT` accept it.

## The built-in ones

`INT`, `BOOL`, `CHAR`, `FLTD` and `TUP` are all immutable classes. Nothing
about them is special: they are written in Sather in the library the same
way, and behave the way they do for the reasons above.
