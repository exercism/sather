# Case Statements

```sather
   case hours
   when 1 then return 300;
   when 2, 3 then return 500;
   else return 900;
   end;
```

## How it matches

The value after `case` is compared with each `when` value using `=`, top to
bottom. The first match runs, and only that one. The remaining `when` parts
are skipped, and execution continues after the `end`.

Any type that supports `=` may be used: `INT`, `CHAR`, `STR`, `BOOL`.

## The else

An unmatched `case` with no `else` raises a fatal error at run time. Always
write one. When the remaining cases genuinely should not happen, say so
there rather than leaving it out:

```sather
   else
      raise "unknown coin: " + cents;
   end;
```

`raise` comes later; until then, returning a sensible default is fine.

## When to prefer if

`case` compares one value against constants. Anything else wants `if`:

```sather
   -- ranges
   if minutes < 30 then ... elsif minutes < 120 then ... end;

   -- more than one value at a time
   if paid and minutes < 120 then ... end;
```

Trying to force a range into a `case` produces something longer and worse
than the `if` it replaced.

## Case as an expression

`case` is a statement, not an expression, so this is not Sather:

```sather
   -- wrong
   charge := case hours when 1 then 300 else 900 end;
```

Return from inside each arm, or assign to a variable inside each arm.
