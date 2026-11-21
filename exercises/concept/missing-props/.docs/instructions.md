# Instructions

You are running the props table for the school play. The props are a map
from a prop's name to how many of it there are.

Before the curtain goes up, the cast come to ask whether a prop can be
taken. You check the table and tell them; you do not hand anything over
yet. None of these tasks changes the map.

All three tasks go in the `MISSING_PROPS` class.

## 1. How many have we got?

Return how many of a prop there are. If the prop is not on the table at all,
raise the string `"Unknown prop: "` followed by its name.

```sather
MISSING_PROPS::count_of(props, "crown")
-- => 2

MISSING_PROPS::count_of(props, "sword")
-- raises "Unknown prop: sword"
```

Note the difference between nought of something and no such thing. A prop
listed with nought is known about; it has simply run out.

## 2. Can one be taken?

Return how many there would be left if one were taken. Do not change the
map: this is only a check. If the prop is listed but there are none, raise
`"Out of "` followed by its name.

```sather
MISSING_PROPS::take_one(props, "crown")
-- => 1

MISSING_PROPS::take_one(props, "lantern")
-- raises "Out of lantern"
```

A prop that is not on the table at all should still raise
`"Unknown prop: ..."`, and you should not have to write that message twice.

## 3. Report back

Return a message rather than raising, whatever happens. This is the answer
read back to the cast member, and like task 2 it leaves the map alone.

```sather
MISSING_PROPS::report(props, "crown")
-- => "Took crown, 1 left"

MISSING_PROPS::report(props, "lantern")
-- => "Out of lantern"

MISSING_PROPS::report(props, "sword")
-- => "Unknown prop: sword"
```

When one can be taken, the message is `"Took "`, the name, `", "`, how
many would be left, and `" left"`. When it does not, the message is exactly what was
raised.
