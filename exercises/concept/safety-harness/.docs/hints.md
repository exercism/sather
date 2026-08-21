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
- The tests are built without `-chk`, so a wrong contract will not fail
  them. Write them for the reader.

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
