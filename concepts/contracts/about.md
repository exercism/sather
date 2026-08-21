# Contracts

```sather
   spare_capacity(load : INT) : INT
      pre load >= 0 and load <= limit
      post result >= 0
   is
      return limit - load;
   end;
```

| Clause | Says | Whose fault if broken |
| --- | --- | --- |
| `pre` | what must hold on entry | the caller's |
| `post` | what holds on return | the routine's |

Both take a `BOOL`, and both may use the routine's arguments and the
object's attributes. `post` may also use `result`, the value being returned.

## assert

Inside a routine body, `assert` states something that must be true at that
point:

```sather
      assert load <= limit;
```

It is checked under the same switch as the others.

## Class invariants

A class may state something true of every object of it between calls:

```sather
   invariant : BOOL is
      return checks >= 0 and limit > 0;
   end;
```

Checked on entry to and exit from every public routine, when checking is on.

## Switching it on

| Flag | Checks |
| --- | --- |
| `-chk` | everything: pre, post, assert, invariant, bounds, arithmetic |
| `-chk_no` | nothing |

Note that `-chk_pre` on its own does *not* turn on precondition checking in
this compiler; `-chk` is what works. A violation prints the routine and the
source line and stops the program. It is not an exception, and `protect`
will not catch it.

The usual arrangement is to develop and test with `-chk` and ship without,
so the checks cost nothing in the shipped program. That only pays if the
tests actually exercise the paths.

## What makes a good contract

Say what the routine needs, not how it works:

```sather
   pre load >= 0 and load <= limit        -- yes
   pre load /= 47                         -- what?
```

A `post` that restates the body teaches nobody anything:

```sather
   post result = limit - load             -- says the body twice
   post result >= 0                       -- says something worth knowing
```

## Inheritance

A subtype may weaken a `pre` and strengthen a `post` — accept more, promise
more — but never the reverse, or code written against the supertype would
break. That is the rule contracts exist to make checkable.
