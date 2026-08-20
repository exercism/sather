# Case Statements

```sather
   case zone
   when 0 then return 0;
   when 1, 2 then return 550;
   else return 920;
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
      raise "unknown zone: " + zone;
   end;
```

`raise` comes later; until then, returning a sensible default is fine.

## When to prefer if

`case` compares one value against constants. Anything else wants `if`:

```sather
   -- ranges
   if age < 13 then ... elsif age < 16 then ... end;

   -- more than one value at a time
   if score >= 8 and sings then ... end;
```

Trying to force a range into a `case` produces something longer and worse
than the `if` it replaced.

## Case as an expression

`case` is a statement, not an expression, so this is not Sather:

```sather
   -- wrong
   fare := case zone when 1 then 550 else 920 end;
```

Return from inside each arm, or assign to a variable inside each arm.
