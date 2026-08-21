# Instructions

You are tramping in New Zealand and taking bearings off a compass. A bearing
is a whole number of degrees, and it is a value: turning by 20 degrees does
not change the bearing you took, it gives you a different one.

Write an `immutable class BEARING`. The stub gives you the class header and
its attribute.

## 1. Take a bearing

`create` takes a number of degrees and gives a bearing. Degrees run from 0
to 359, so anything outside comes back round: 370 is 10, and -10 is 350.

```sather
#BEARING(370).degrees
-- => 10
#BEARING(-10).degrees
-- => 350
```

## 2. Turn

`turned` takes a number of degrees to turn by and answers the new bearing.
Turning by a negative number turns the other way. The bearing it was called
on is unchanged.

```sather
#BEARING(350).turned(20).degrees
-- => 10
```

## 3. Compare

`is_eq` takes another bearing and answers whether they are the same. Once it
exists, `=` works on bearings.

```sather
#BEARING(10) = #BEARING(370)
-- => true
```

## 4. Name the point

`point` answers the compass point the bearing is nearest to, as one of
`"N"`, `"NE"`, `"E"`, `"SE"`, `"S"`, `"SW"`, `"W"`, `"NW"`.

Each point covers 45 degrees, centred on its exact bearing: north runs from
337.5 through 0 to 22.5, north-east from 22.5 to 67.5, and so on. Since
bearings here are whole numbers, a bearing of 22 is `"N"` and 23 is `"NE"`.

```sather
#BEARING(0).point
-- => "N"
#BEARING(90).point
-- => "E"
#BEARING(225).point
-- => "SW"
```

## 5. Write it down

`str` answers the degrees and the point, like `"90 degrees (E)"`.

```sather
#BEARING(90).str
-- => "90 degrees (E)"
```
