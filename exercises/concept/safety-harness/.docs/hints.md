# Hints

## General

- A contract goes after the return type and before the `is`:

  ```sather
     fee(withdrawals : INT) : INT
        pre withdrawals >= 0
     is
        ...
     end;
  ```

- Inside a contract you may use the arguments and the object's attributes,
  so `limit` is available.
- The tests are built with `-chk`, so contracts are checked. A contract that
  a test breaks stops the whole run with the routine's name, rather than
  failing one test. A contract that is too weak passes, though: write them
  for the reader as much as for the checker.

## 1. Rig a harness

- A `pre` on `create`, about its argument. Nought is not allowed, so the
  comparison is a strict one.
- The body is the usual `new`, set the attribute, return it.

## 2. How much is spare?

- Two conditions on the load in one `pre`, joined with `and`: one for each
  end of the range a load may be in.
- The `post` says the answer is never negative. That follows from the `pre`,
  which is what makes it worth saying — it records why the answer can be
  trusted.

## 3. How full is it?

- The same `pre` on the load as the first half of task 2's, and the same
  `post` as task 2's.
- Multiply by 100 before dividing by the limit. Dividing first would throw
  everything away, as it would in `tuning-the-strings`.

## 4. Is it safe?

- No `pre` at all: the whole point is that any load may be asked about.
- The `post` restates the question: compare `result` with the question the
  body asks. Brackets round the question, because `=` is being used twice
  for different things.

## 5. Always rated

- `invariant : BOOL is ... end;`, an ordinary routine with that exact name.
  No `pre` or `post`: it *is* the contract.
- Ask `void(self)` first, then the condition on the rating, joined with
  `or`. `or` stops at the first true part, so `limit` is never read from a
  void `self`.
