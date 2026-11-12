# Hints

## General

- The guide's type is `FMAP{STR,STR}` — it maps a name to a habitat, and
  both are strings. Write that type out in full in every routine that takes
  one.

## 1. Is it in the guide?

- `has_ind` gives the answer directly. Return it; no `if` is needed.

## 2. Where does it live?

- `get` on a missing key does not complain — it answers a void string, which
  goes wrong somewhere else entirely. Ask `has_ind` first.
- An `if` with an `else`: fetch in one branch, and answer the fallback the
  instructions give in the other.

## 3. Add an entry

- `insert` takes the key and then the target, and answers the map to use
  from now on. Return that answer; nothing more is needed.
- There is nothing to do about an animal already listed: `insert` replaces.
- There is nothing to do about an empty guide either. Inserting into one is
  how a map starts.

## 4. How many animals?

- `.size`.

## 5. Which habitats?

- Start from an empty `FSET{STR}`.
- `target!` walks a map's targets, which here are the habitats. Insert each
  one into the set, assigning the answer back every time.
- Repeats need no handling. A set keeps one copy, which is the whole reason
  the answer is a set and not an array.
