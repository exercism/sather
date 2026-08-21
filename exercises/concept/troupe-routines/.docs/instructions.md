# Instructions

Every routine the dance troupe performs is built on the same warm-up, and
then goes its own way.

The stub gives you `WARM_UP`. Write three more classes below it.

## 1. The jazz routine

`JAZZ_ROUTINE` takes everything from `WARM_UP` unchanged, and adds nothing.

```sather
JAZZ_ROUTINE::counts
-- => 8
JAZZ_ROUTINE::describe
-- => "8 counts"
```

## 2. The tap routine

`TAP_ROUTINE` takes `counts` from `WARM_UP` but describes itself its own
way. Leave `describe` out of the include and write a new one.

```sather
TAP_ROUTINE::counts
-- => 8
TAP_ROUTINE::describe
-- => "Tap: 8 counts"
```

## 3. The finale

`FINALE` takes `counts` from `WARM_UP` under the name `warm_up_counts`, and
leaves `describe` out. It then has its own `counts`, which is twice the
warm-up's, and its own `describe`.

```sather
FINALE::warm_up_counts
-- => 8
FINALE::counts
-- => 16
FINALE::describe
-- => "Finale: 16 counts"
```

Note what this shows: `FINALE::counts` is not `WARM_UP::counts`, and both
are available under different names in the same class.
