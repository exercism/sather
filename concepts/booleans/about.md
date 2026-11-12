# Booleans

`BOOL` holds one of two values, `true` and `false`.

```sather
   ready : BOOL is
      return true;
   end;
```

## Comparison

| Operator | Asks | Example |
| --- | --- | --- |
| `=` | same? | `days_out = 21` |
| `/=` | different? | `days_out /= 21` |
| `<` | less than | `days_out < 21` |
| `<=` | less than or equal | `days_out <= 21` |
| `>` | greater than | `days_out > 21` |
| `>=` | greater than or equal | `days_out >= 21` |

These work on numbers, and `=` and `/=` work on strings too.

## The three operators

| Operator | Written | True when |
| --- | --- | --- |
| and | `a and b` | both are true |
| or | `a or b` | at least one is true |
| not | `~a` | `a` is false |

`and` and `or` are **short-circuiting**: `a and b` does not bother looking
at `b` once `a` turns out false, because the answer is already settled.
Likewise `a or b` stops if `a` is true. That matters when the right-hand
side is expensive, or would go wrong if it ran.

## Returning a comparison directly

A routine whose whole job is to ask a question should return the question,
not pick an answer with a conditional:

```sather
   -- say this
   overdue(days_out : INT) : BOOL is
      return days_out > 21;
   end;
```

Writing `if days_out > 21 then return true else return false end` takes three
lines to say what the comparison already said, and every experienced reader
will notice.

## Precedence

`~` binds tightest, then `and`, then `or`. So

```sather
~a and b or c
```

means `((~a) and b) or c`. Brackets cost nothing to write, and are worth
it whenever a reader would otherwise have to recall that order to follow
the line.
