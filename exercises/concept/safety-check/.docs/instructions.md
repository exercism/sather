# Instructions

Nobody gets on the trapeze at the circus until the safety checks pass.
You are writing the checks down so the same rules apply to everybody.

All five tasks go in the `SAFETY_CHECK` class.

## 1. Is the mat ready?

The mat is ready only when it is both down and clean.

```sather
SAFETY_CHECK::mat_ready(true, false)
-- => false
```

## 2. Is there something to land on?

There has to be a mat below, or a net below. Either will do, and having
both is fine.

```sather
SAFETY_CHECK::something_below(false, true)
-- => true
```

## 3. Who still needs the briefing?

Anybody who has not been briefed needs the briefing.

```sather
SAFETY_CHECK::needs_briefing(false)
-- => true
```

## 4. Is this performer old enough?

Trapeze is for performers of 13 and over.

```sather
SAFETY_CHECK::old_enough(13)
-- => true
```

## 5. Put it all together

A performer is cleared for the trapeze when they are old enough, they have
been briefed, and the mat is ready.

```sather
SAFETY_CHECK::cleared(14, true, true, true)
-- => true
```

The four arguments are the age, whether they have been briefed, whether the
mat is down, and whether the mat is clean.
