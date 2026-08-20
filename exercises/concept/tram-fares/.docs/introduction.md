# Case Statements

When one value is compared against a list of possibilities, a chain of
`elsif`s says the same thing over and over:

```sather
   if zone = 0 then
      return 0;
   elsif zone = 1 then
      return 550;
   elsif zone = 2 then
      return 370;
   else
      return 920;
   end;
```

`case` says it once:

```sather
   case zone
   when 0 then return 0;
   when 1 then return 550;
   when 2 then return 370;
   else return 920;
   end;
```

The value goes after `case`. Each `when` gives a value to compare it
against, and the first one that matches runs.

## Several values in one when

A `when` may list values, separated by commas:

```sather
   case day
   when "Sat", "Sun" then return "Weekend";
   when "Mon", "Tue", "Wed", "Thu", "Fri" then return "Weekday";
   else return "Unknown";
   end;
```

This works on whole numbers, characters and strings — anything that can be
compared with `=`.

## The else is not optional

**A `case` that matches nothing and has no `else` is an error that stops the
program when it happens.**

That is different from `if`, where leaving off the `else` simply means
nothing happens. It is also different from most languages, where an
unmatched `case` quietly does nothing.

So every `case` needs an `else`, even when you are sure the `when` parts
already cover every value. A fourth zone gets added later, the `case` is not
updated to match, and the program stops on the first passenger who uses it.

## Only one when runs

When a `when` matches, the statements after its `then` run and the `case` is
finished — the program carries on after the `end`. The `when` parts below it
are never looked at, so there is nothing you have to write to stop the next
one from running as well.
