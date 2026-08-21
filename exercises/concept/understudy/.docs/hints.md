# Hints

## 1. Two ways of saying a line

- `.upper` and `.lower` work on a whole string, not only a character.
- `whisper` joins `"..."` on each end of the lowered line.

## 2. Rehearse a line

- The argument type is written `ROUT{STR}:STR` — the argument types in
  braces, the answer after the colon.
- The body is one line: `return part.call(line);`
- `rehearse` must not mention `shout` or `whisper`. Not knowing is the whole
  point of taking a bound routine.

## 3. The whole scene

- A loop and an `FSTR`, as in `rehearsal-script`.
- Call `part.call(...)` on each line, and put the `" "` before every line
  except the first.

## 4. Hand back a way of saying things

- The return type is `ROUT{STR}:STR`, exactly as the argument type was in
  task 2.
- `bind(shout(_))` inside the class — no class name needed, as with any
  routine called from its own class.
- `return bind(...)` does not parse. A `bind` has to go on the right of an
  assignment first:

  ```sather
     part : ROUT{STR}:STR;
     if ... then part := bind(shout(_)); else ... end;
     return part;
  ```

- Two cases, so an `if`, or a `case` with its `else`.

## 5. Fix an argument

- `repeat` itself is an ordinary routine: a loop, an `FSTR`, and
  `1.upto!(times)`.
- `doubler` binds it with the number written out and the line left as a
  hole: `bind(repeat(2, _))`. As in task 4, put it in a variable and return
  that.
- Only the `_` becomes an argument of the bound routine, which is why
  `bind(repeat(2, _))` has type `ROUT{STR}:STR` and not `ROUT{INT,STR}:STR`.
