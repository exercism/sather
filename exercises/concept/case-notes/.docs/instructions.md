# Instructions

A detective's notebook fills up as a case goes on, and empties again as
lines of enquiry are ruled out.

All five tasks go in the `CASE_NOTES` class.

## 1. Open a case

Return a new, empty notebook.

```sather
notes ::= CASE_NOTES::new_case;
notes.size
-- => 0
```

## 2. Write a clue down

Add a clue to the end of the notebook. This answers nothing — it changes the
notebook it is given.

```sather
CASE_NOTES::add_clue(notes, "muddy boots");
notes.size
-- => 1
```

Promise in the header that the notebook ends up one clue longer than it
was. In a postcondition, `initial(...)` is the value something had when the
routine was called:

```sather
      post notes.size = initial(notes.size) + 1
```

## 3. How many clues?

```sather
CASE_NOTES::clue_count(notes)
-- => 1
```

## 4. Rule one out

Take the clue at a position out of the notebook. Everything after it moves
up. This also answers nothing.

```sather
CASE_NOTES::rule_out(notes, 0);
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
