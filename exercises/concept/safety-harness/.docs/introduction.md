# Contracts

A routine's arguments and return type say what *kind* of thing goes in and
comes out. They cannot say that a number of withdrawals must not be
negative, or that a bank account never reports more dollars than it holds.

A **contract** says those things, in the routine's own header, where anybody
reading it will see them.

## pre

`pre` states what must be true when the routine is called. It goes between
the return type and the `is`.

```sather
   fee(withdrawals : INT) : INT
      pre withdrawals >= 0
   is
      return withdrawals * 50;
   end;
```

That is a demand on the **caller**: do not call this with a negative number
of withdrawals. `create` may have a `pre` like any other routine.

## post

`post` states what will be true when the routine answers. Inside it,
`result` is the value being returned.

```sather
   whole_dollars : INT
      pre balance >= 0
      post result * 100 <= balance
   is
      return balance / 100;
   end;
```

That is a promise to the caller. A routine with both is a bargain: give me
this, and I will give you that.

Several conditions join with `and`, as any booleans do:

```sather
      pre rate >= 0 and rate <= 20
```

A `post` on a routine that answers a `BOOL` can compare `result` with a
question. The question goes in brackets, because `=` is doing two different
jobs on the one line:

```sather
      post result = (balance < 0)
```

## Class invariants

A class may state something true of every object of it between calls, in a
routine named `invariant` that answers a `BOOL`:

```sather
   invariant : BOOL is
      return void(self) or (overdraft >= 0 and balance + overdraft >= 0);
   end;
```

It is checked on entry to and exit from every public routine. That includes
entry to `create`, when there is no object yet and `self` is void. Reading
an attribute from a void `self` stops the program. `or` stops at the first
true part, so asking `void(self)` first keeps the rest from being read.

## Contracts are not exceptions

A raised exception is for something that can happen. A broken contract means
a **bug** — somebody called the routine wrongly, or the routine did not do
what it said.

So a broken contract does not raise something catchable. When contract
checking is switched on, the program stops and prints which routine, and
which condition. When it is switched off, the condition is not even tested,
and the program runs on into whatever nonsense follows.

That is why a contract is a statement about correctness rather than a way of
handling bad input. If bad input is expected, check it and `raise`. If bad
input means the caller is broken, say so with `pre`.

## Switching checking on

This Sather checks contracts when the compiler is given `-chk`:

```
sacomp -chk mine.sa -main MAIN -o mine
```

Without it, `pre` and `post` are documentation the compiler has read and
agreed is well-formed, and nothing more. The tests for this exercise are
built with `-chk`, so a contract that a test breaks stops the run. They
cannot show that a contract is strong enough, though: they check that the
routines do the right thing when used properly.
