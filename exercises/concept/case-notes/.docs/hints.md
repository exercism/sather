# Hints

## General

- The type is `LIST{STR}` throughout — a list of strings. Write it out in
  full wherever a notebook goes in or comes out.

## 1. Open a case

- `#LIST{STR}` makes an empty one. The routine takes no arguments and
  returns `LIST{STR}`.

## 2. Write a clue down

- `append` is the routine, and it answers nothing — so this routine has no
  return type either: `add_clue(notes : LIST{STR}, clue : STR) is`.
- Do not assign the result of `append` anywhere. Unlike `FMAP::insert`,
  there is no result.

## 3. How many clues?

- `.size`.

## 4. Rule one out

- `remove_index` takes the position. No return type again.

## 5. Read the case back

- A loop over `notes.elt!` and an `FSTR`, as in `rehearsal-script`.
- The `"; "` goes before every clue except the first, which is what makes an
  empty notebook come out as the empty string with no special handling.
