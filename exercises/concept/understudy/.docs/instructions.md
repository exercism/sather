# Instructions

Every part in the school play has an understudy: somebody who can step in
and do what the part needs, without the stage manager knowing who they are.

All five tasks go in the `UNDERSTUDY` class. The first two are ordinary
routines that later tasks will bind.

## 1. Two ways of saying a line

Write `shout`, which returns the line in capitals, and `whisper`, which
returns it in small letters with `"..."` on each end.

```sather
UNDERSTUDY::shout("who's there")
-- => "WHO'S THERE"
UNDERSTUDY::whisper("Who's There")
-- => "...who's there..."
```

## 2. Rehearse a line

`rehearse` takes a line and a way of saying it, and returns the result. Its
second argument has type `ROUT{STR}:STR`.

```sather
UNDERSTUDY::rehearse("who's there", bind(UNDERSTUDY::shout(_)))
-- => "WHO'S THERE"
```

## 3. The whole scene

`run_scene` takes an array of lines and a way of saying them, and returns
them all said that way, joined with `" "`.

```sather
UNDERSTUDY::run_scene(|"Enter", "Exit"|, bind(UNDERSTUDY::shout(_)))
-- => "ENTER EXIT"
```

An empty scene is the empty string.

## 4. Hand back a way of saying things

`understudy_for` takes the name of a style — `"shout"` or anything else —
and returns a `ROUT{STR}:STR`. `"shout"` gives the shouting one; anything
else gives the whispering one.

```sather
part ::= UNDERSTUDY::understudy_for("shout");
part.call("who's there")
-- => "WHO'S THERE"
```

## 5. Fix an argument

Write `repeat`, which takes a number of times and a line and returns the
line that many times over with nothing between:

```sather
UNDERSTUDY::repeat(3, "Ha")
-- => "HaHaHa"
```

Then write `doubler`, which takes no arguments and returns a `ROUT{STR}:STR`
that repeats whatever it is given twice — by binding `repeat` with the
number already filled in.

```sather
UNDERSTUDY::doubler.call("Ha")
-- => "HaHa"
```
