# Case Statements

When one value is compared against a list of possibilities, a chain of
`elsif`s says the same thing over and over:

```sather
   if hours = 1 then
      return 300;
   elsif hours = 2 then
      return 500;
   elsif hours = 3 then
      return 650;
   else
      return 900;
   end;
```

`case` says it once:

```sather
   case hours
   when 1 then return 300;
   when 2 then return 500;
   when 3 then return 650;
   else return 900;
   end;
```

The value goes after `case`. Each `when` gives a value to compare it
against, and the first one that matches runs.

## Several values in one when

A `when` may list values, separated by commas:

```sather
   case cents
   when 10, 20, 50 then return "Silver";
   when 100, 200 then return "Gold";
   else return "Rejected";
   end;
```

This works on whole numbers, characters and strings — anything that can be
compared with `=`. A string `when` looks the same, with the strings in
double quotes; a character goes in single quotes, as `'Y'`.

```sather
   case street
   when "Quay", "Customs" then return "Two hours";
   else return "All day";
   end;
```

The value after `case` need not be a variable. Any expression will do,
including a call to another routine.

## The else is not optional

**A `case` that matches nothing and has no `else` is an error that stops the
program when it happens.**

That is different from `if`, where leaving off the `else` simply means
nothing happens. It is also different from most languages, where an
unmatched `case` quietly does nothing.

So every `case` needs an `else`, even when you are sure the `when` parts
already cover every value. A new coin is minted, the `case` is not updated
to match, and the program stops on the first driver who puts one in.

## Only one when runs

When a `when` matches, the statements after its `then` run and the `case` is
finished — the program carries on after the `end`. The `when` parts below it
are never looked at, so there is nothing you have to write to stop the next
one from running as well.
