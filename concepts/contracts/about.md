# Contracts

```sather
   yearly_interest(rate : INT) : INT
      pre balance >= 0 and rate >= 0 and rate <= 20
      post result <= balance
   is
      return balance * rate / 100;
   end;
```

| Clause | Says | Whose fault if broken |
| --- | --- | --- |
| `pre` | what must hold on entry | the caller's |
| `post` | what holds on return | the routine's |

Both take a `BOOL`, and both may use the routine's arguments and the
object's attributes. `post` may also use `result`, the value being returned.

## initial

A routine that changes something, rather than answering something, has no
`result` to make promises about. Its promise is about the change, and for
that `post` can look back: `initial(...)` is the value an expression had
when the routine was called.

```sather
   withdraw(amount : INT)
      pre amount > 0 and amount <= balance + overdraft
      post balance = initial(balance) - amount
   is
      balance := balance - amount;
   end;
```

`initial` is allowed only in `post`.

## assert

Inside a routine body, `assert` states something that must be true at that
point:

```sather
      assert balance + overdraft >= 0;
```

It is checked under the same switch as the others.

## Class invariants

A class may state something true of every object of it between calls, in a
routine named `invariant`:

```sather
   invariant : BOOL is
      return void(self) or (overdraft >= 0 and balance + overdraft >= 0);
   end;
```

Checked on entry to and exit from every public routine, when checking is on.

That includes entry to `create`, when there is no object yet and `self` is
void. Reading an attribute from a void `self` stops the program, which is
what the `void(self) or` allows for: `or` stops at the first true part.

An `immutable class` may declare an invariant, but this compiler never
checks it. For a value, put the promise in `post` on the routines that make
one.

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
   pre amount > 0 and amount <= balance   -- yes
   pre amount /= 47                       -- what?
```

A `post` that restates the body teaches nobody anything:

```sather
   post result = balance * rate / 100     -- says the body twice
   post result <= balance                 -- says something worth knowing
```

## Inheritance

A subtype may weaken a `pre` and strengthen a `post` — accept more, promise
more — but never the reverse, or code written against the supertype would
break. That is the rule contracts exist to make checkable.
