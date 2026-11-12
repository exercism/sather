# Immutable Classes

A `SCOREBOARD` is a thing that changes. Two names for one scoreboard see the
same score, because there is only one board and both names point at it.

A leg of a road trip is not like that. Bath to York does not become
something else; it simply *is*. Numbers behave that way, and so do strings
— and so can classes of your own.

## immutable

```sather
immutable class LEG is

   readonly attr origin, destination : STR;

end; -- class LEG
```

Two words change everything. An object of an immutable class is a **value**,
not a thing pointed at:

- it is copied when assigned or passed, so nobody else can change yours;
- it can never be void;
- and its attributes cannot be assigned to.

## Changing one by making another

Since `destination := "York"` is not allowed, `attr` gives something else:
a routine taking the new value and answering **a new object** with it
changed.

```sather
   leg := leg.destination("York");      -- not leg.destination := "York"
```

The original is untouched. That is the whole idiom, and it is how `create`
is written:

```sather
   create(from, to : STR) : SAME is
      leg : SAME;                   -- starts with every attribute empty
      return leg.origin(from).destination(to);
   end;
```

There is no `new` here. An immutable object always exists, so `leg : SAME`
already is one, with every attribute at its empty value. Each attribute
routine answers a new leg, so the second is called on what the first
answered.

A routine that "changes" a leg therefore returns a new one:

```sather
   home : SAME is
      return #LEG(destination, origin);
   end;
```

`#LEG("Bath", "York").home` is the leg from York back to Bath. The leg it
was called on is still Bath to York.

## Comparing

Values are compared by what they hold, not by which object they are — but
you have to say how. Write `is_eq`, and `=` will use it:

```sather
   is_eq(leg : SAME) : BOOL is
      return origin = leg.origin and destination = leg.destination;
   end;
```

Without it, `=` on two legs will not compile.

## Which to choose

Use an immutable class when the thing has no identity and nothing about it
can sensibly change: a leg of a journey, a point, a date, a length. Use an
ordinary class when the thing is one particular thing that things happen to:
a scoreboard, a harness, a file.

The test is whether "the same" means "equal" or "the very same one".
