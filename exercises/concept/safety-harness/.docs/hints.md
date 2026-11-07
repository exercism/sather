# Hints

## General

- A contract goes after the return type and before the `is`:

  ```sather
     spare_capacity(load : INT) : INT
        pre load >= 0
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

- `pre kg > 0`, on `create`.
- The body is the usual `new`, set the attribute, return it.

## 2. How much is spare?

- Two conditions joined with `and`: `pre load >= 0 and load <= limit`.
- `post result >= 0`. That follows from the `pre`, which is what makes it
  worth saying — it records why the answer can be trusted.

## 3. How full is it?

- `pre load >= 0` and `post result >= 0`.
- `load * 100 / limit`, in that order. Dividing first would throw everything
  away, as it would in `tuning-the-strings`.

## 4. Is it safe?

- No `pre` at all: the whole point is that any load may be asked about.
- The `post` restates the question: `post result = (load <= limit)`.
  Brackets, because `=` is being used twice for different things.

## 5. Always rated

- `invariant : BOOL is ... end;`, an ordinary routine with that exact name.
  No `pre` or `post`: it *is* the contract.
- `void(self) or limit > 0`. `or` stops at the first true part, so `limit`
  is never read from a void `self`.
