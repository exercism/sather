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

`label_pair` has no idea what `label` does. That is the point: given a
second routine of the same shape,

```sather
   lid_label(flower : STR) : STR is return flower.upper + " HONEY"; end;
```

it can be handed either one, or anything else that takes a `STR` and
answers a `STR`:

```sather
   label_pair("Rata", "Kamahi", bind(jar_label(_)))   -- "Rata honey and Kamahi honey"
   label_pair("Rata", "Kamahi", bind(lid_label(_)))   -- "RATA HONEY and KAMAHI HONEY"
```

## Handing one back

A routine can answer a bound routine, too. There is one snag, and it is in
this compiler rather than in the language: it cannot read `bind` straight
after `return`.

```sather
   honey_label : ROUT{STR}:STR is
      return bind(jar_label(_));          -- does not compile
   end;
```

The error says `'end' expected, but found 'bind'`, which is no help at all.
What has happened is that `return` did not recognise `bind` as the start of
a value, so it took this for a `return` with nothing after it.

Brackets fix it, because a bracket always starts a value:

```sather
      return (bind(jar_label(_)));        -- yes
```

So does putting the `bind` in a variable first, and returning that:

```sather
      label : ROUT{STR}:STR := bind(jar_label(_));
      return label;                       -- yes
```

The same goes for `yield`. Anywhere else, such as on the right of `:=` or as
an argument, `bind` needs no help.

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
