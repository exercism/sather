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
| `=` | same? | `age = 13` |
| `/=` | different? | `age /= 13` |
| `<` | less than | `age < 13` |
| `<=` | less than or equal | `age <= 13` |
| `>` | greater than | `age > 13` |
| `>=` | greater than or equal | `age >= 13` |

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
   old_enough(age : INT) : BOOL is
      return age >= 13;
   end;
```

Writing `if age >= 13 then return true else return false end` takes three
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
