# Exceptions

Some routines cannot answer. Asked for a prop that is not on the table,
`count_of` has no number to give — and nought would be a lie, because nought
means "we have none of those", not "there is no such thing".

An **exception** is how a routine says it cannot answer.

## Raising

`raise` abandons the routine and hands a value to whoever called it.

```sather
   count_of(props : FMAP{STR,INT}, prop : STR) : INT is
      if ~props.has_ind(prop) then
         raise "Unknown prop: " + prop;
      end;
      return props.get(prop);
   end;
```

Nothing after a `raise` runs. The routine does not return, so there is no
answer to check and no way for the caller to carry on as though there were.

The value raised is usually a string saying what went wrong.

## Catching

`protect` runs a piece of code, ready for it to raise.

```sather
   protect
      taken ::= count_of(props, prop);
      #OUT + "There are " + taken;
   when $STR then
      #OUT + "Cannot: " + exception.str;
   end;
```

If nothing raises, the part after `protect` runs and the `when` arm is
skipped. If something raises, the rest of the `protect` part is abandoned
and the matching `when` runs instead.

`when $STR then` catches a raised string. `exception` is the value that was
raised, available inside the arm.

## Passing through

A routine that does not catch an exception does not have to do anything
about it. It travels outward, through every caller, until something catches
it:

```sather
   take_one(props : FMAP{STR,INT}, prop : STR) : INT is
      -- If this raises, take_one raises too. Nothing here says so.
      have ::= count_of(props, prop);
      ...
   end;
```

That is the point of exceptions. The routine that notices the problem and
the routine that knows what to do about it are usually not the same routine,
and everything in between can ignore it.
