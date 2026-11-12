# Bound Routines

Everything so far has passed *values* around: numbers, strings, objects. A
**bound routine** lets you pass around a routine itself — something to be
called later, by code that does not know what it is.

A beekeeper's labelling machine is the idea exactly: it holds a way of
writing a label, without knowing what the label will say.

## Making one

`bind` takes a call with holes in it, written `_`:

```sather
   jar_label(flower : STR) : STR is return flower + " honey"; end;

   ...

   label ::= bind(jar_label(_));
```

`label` is now a value like any other. Calling it happens later:

```sather
   label.call("Clover")      -- "Clover honey"
```

## The type

The type of a bound routine is `ROUT`, with the argument types in braces and
the return type after a colon:

```sather
   label : ROUT{STR}:STR := bind(jar_label(_));
```

Read `ROUT{STR}:STR` as "a routine taking a `STR` and answering a `STR`".

| Written | Means |
| --- | --- |
| `ROUT{STR}:STR` | takes a `STR`, answers a `STR` |
| `ROUT{INT,INT}:BOOL` | takes two `INT`s, answers a `BOOL` |
| `ROUT{STR}` | takes a `STR`, answers nothing |
| `ROUT:INT` | takes nothing, answers an `INT` |

Since it is a type, it can be an argument:

```sather
   label_pair(first, second : STR, label : ROUT{STR}:STR) : STR is
      return label.call(first) + " and " + label.call(second);
   end;
```

`label_pair` has no idea what `label` does. That is the point: it can be
handed `jar_label`, or a routine that answers `flower.upper`, or anything
else of that shape. (`.upper` and `.lower` work on a whole string, not only
on a character: `"Rata".upper` is `"RATA"`.)

## Filling in some of the arguments

Not every argument has to be a hole. Anything written out is fixed when the
bind happens:

```sather
   price_tag(flower : STR, grams : INT) : STR is
      return flower + " " + grams + "g";
   end;

   small ::= bind(price_tag(_, 250));      -- ROUT{STR}:STR
```

`small.call("Manuka")` is `"Manuka 250g"`. `small` takes only the flower,
because the `250` is already decided. The value
is worked out at the moment of binding and kept, so changing the variable it
came from afterwards makes no difference.

This is how one general routine becomes many specific ones.

## Binding the object too

For a routine on an object, the object is the first thing in the call and
can be fixed or left as a hole:

```sather
   bind(hive.add_frame)      -- this hive's, always
   bind(_.add_frame)         -- whichever hive is handed in later
```
