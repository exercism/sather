# Hints

## General

- There is no `new` in an immutable class. `create` starts with a variable
  of the class, which already exists:

  ```sather
     create(d : INT) : SAME is
        b : SAME;
        return b.degrees(...);
     end;
  ```

- `b.degrees(x)` does not change `b`. It answers a new bearing, which is why
  it is the thing being returned.

## 1. Take a bearing

- `%` brings a number into range, but `-10 % 360` is `350` only because
  Sather's `%` never answers negative for a positive right-hand side. So
  `d % 360` is enough on its own.

## 2. Turn

- Add the turn to the degrees and make a new bearing from the total:
  `#BEARING(degrees + by)`.
- `create` already brings the answer back into range, so there is nothing to
  do about turning past north.

## 3. Compare

- One line: compare the two `degrees`.
- The argument's type is `SAME`, and you read its attribute the usual way:
  `other.degrees`.

## 4. Name the point

- The trick is to shift by half a segment before dividing, so that each
  point's *centre* is what it is measured from:
  `((degrees + 22) / 45) % 8` gives 0 for north, 1 for north-east, and so
  on.
- Then a `case` on that number, with the eight names — and an `else`, which
  `case` always needs even when the eight arms cover every possible value.

## 5. Write it down

- `+` joins the pieces, but only a string may have things added to it. The
  number comes first here, so it needs `degrees.str` to start the join off.
  `"a" + 1` is fine; `1 + "a"` does not compile.
- Call `point` rather than working the name out again.
