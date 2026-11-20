# Instructions

A detective's notebook fills up as a case goes on, and empties again as
lines of enquiry are ruled out.

All six tasks go in the `CASE_NOTES` class.

## 1. Open a case

Return a new, empty notebook.

```sather
notes ::= CASE_NOTES::new_case;
notes.size
-- => 0
```

## 2. Write a clue down

Add a clue to the end of the notebook, and answer the notebook to use from
now on.

```sather
notes := CASE_NOTES::add_clue(notes, "muddy boots");
notes.size
-- => 1
```

Promise in the header that the notebook it answers is one clue longer than
the one it was given. In a postcondition, `initial(...)` is the value
something had when the routine was called:

```sather
      post result.size = initial(notes.size) + 1
```

## 3. How many clues?

```sather
CASE_NOTES::clue_count(notes)
-- => 1
```

## 4. Rule one out

Take the clue at a position out of the notebook, and answer the notebook to
use from now on. Everything after it moves up, and the order of the rest
must not change.

```sather
notes := CASE_NOTES::rule_out(notes, 0);
```

Asking to rule out a clue that is not there is a mistake by the caller, so
say so with a precondition: the position must be in the notebook. Then
promise, as in task 2, that the notebook ends up one clue shorter.

## 5. Read the case back

Return every clue in the notebook, joined with `"; "`. An empty notebook
reads as the empty string.

```sather
CASE_NOTES::summary(notes)
-- => "muddy boots; broken window"
```

## 6. Hand the clues over

The case is going to court, and the court wants the clues as a fixed
`ARRAY{STR}`, in the order they are in the notebook.

```sather
CASE_NOTES::clues(notes)
-- => |"muddy boots", "broken window"|
```
