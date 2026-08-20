# Instructions

Auditions for the school play are over and the director needs the decisions
written down.

All four tasks go in the `CASTING_CALL` class.

## 1. The verdict

Every performer is scored out of ten. Eight or more and they are cast; five
to seven and they are recalled; below five they are thanked.

```sather
CASTING_CALL::audition_outcome(8)
-- => "Cast"
CASTING_CALL::audition_outcome(6)
-- => "Recalled"
CASTING_CALL::audition_outcome(2)
-- => "Thank you"
```

## 2. Which group?

Performers under 13 are Juniors. From 13 to 15 they are Middles. Sixteen and
over, Seniors.

```sather
CASTING_CALL::age_group(13)
-- => "Middles"
```

## 3. When to come back

Juniors are recalled at four o'clock, Middles at five, and everybody else at
six.

```sather
CASTING_CALL::callback_time("Middles")
-- => "5pm"
```

The argument is the name of a group, spelled exactly as task 2 spells it.

## 4. What to write on the sheet

Somebody who scored eight or more and can sing is a `"Lead"`. Eight or more
without singing is `"Speaking part"`. Anybody else is `"Chorus"`.

```sather
CASTING_CALL::casting_note(9, true)
-- => "Lead"
CASTING_CALL::casting_note(9, false)
-- => "Speaking part"
CASTING_CALL::casting_note(4, true)
-- => "Chorus"
```
