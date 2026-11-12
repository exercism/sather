# Exceptions

Some routines cannot answer. Asked how long a drink takes to make, when the
café has never heard of that drink, a routine has no number to give — and
nought would be a lie, because nought means "ready at once", not "there is
no such drink".

An **exception** is how a routine says it cannot answer.

## Raising

`raise` abandons the routine and hands a value to whoever called it.

```sather
   brew_minutes(drink : STR) : INT is
      if drink = "espresso" then return 1; end;
      if drink = "pot of tea" then return 4; end;
      raise "Not on the menu: " + drink;
   end;
```

Nothing after a `raise` runs. The routine does not return, so there is no
answer to check and no way for the caller to carry on as though there were.

The value raised is usually a string saying what went wrong.

## Catching

`protect` runs a piece of code, ready for it to raise.

```sather
   protect
      wait ::= brew_minutes(order);
      #OUT + "Ready in " + wait + " minutes";
   when $STR then
      #OUT + "Sorry: " + exception.str;
   end;
```

If nothing raises, the part after `protect` runs and the `when` arm is
skipped. If something raises, the rest of the `protect` part is abandoned
and the matching `when` runs instead.

`when $STR then` catches a raised string. `exception` is the value that was
raised, available inside the arm.

Both parts are ordinary code. Either may `return` from the routine, just as
the code outside a `protect` can.

## Passing through

A routine that does not catch an exception does not have to do anything
about it. It travels outward, through every caller, until something catches
it:

```sather
   table_minutes(first, second : STR) : INT is
      -- If either call raises, table_minutes raises too. Nothing here says
      -- so.
      return brew_minutes(first).max(brew_minutes(second));
   end;
```

That is the point of exceptions. The routine that notices the problem and
the routine that knows what to do about it are usually not the same routine,
and everything in between can ignore it.
