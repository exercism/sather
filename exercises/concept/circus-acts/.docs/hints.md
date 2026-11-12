# Hints

## 1. The three acts

- The class header names the abstract class after `<`, which is read "is
  a".
- Each must define both `name` and `minutes`, exactly as the abstract class
  declares them. Missing one is a compile error naming the routine.
- Each also needs a `create`, or `#` has nothing to call. For the two that
  hold nothing, returning `new` is the whole of it.
- `TRAPEZE` needs an attribute for the height, and a `create` taking it.
- `+` joins a number onto a string, so the name can be built from its pieces
  with no converting.

## 2. The show

- The argument type is `ARRAY{$ACT}`. That is what lets one array hold all
  three kinds.
- `elt!` on the array gives an `$ACT`. Calling `.minutes` on it runs the right
  one by itself — that is dispatch, and it is the point of the exercise. There
  is nothing to check and no `typecase` to write.
- `billing` builds a string in a loop, so `FSTR`, and the `", "` goes before
  every name except the first.
- `longest` keeps the best act so far. Starting the best minutes below any
  real length means the first act always beats it, which handles the empty
  show without a special case: the name stays empty.
