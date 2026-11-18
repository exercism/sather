# Math Functions

Square roots, angles and growth curves are hard to work out with `+`, `-`,
`*` and `/` alone. `FLTD` has routines that work them out for you. Each is
called on the number it works on, with a dot, the same way as `.abs`.

## Square roots and powers

```sather
   9.0d.sqrt              -- 3.0
   2.0d.pow(10.0d)        -- 1024.0, which is 2 to the power 10
```

A ladder 5 metres long, with its foot 3 metres from a wall, reaches
`(5.0d * 5.0d - 3.0d * 3.0d).sqrt` metres up it: `4.0`.

## Pi

`FLTD::pi` is π, the number of times a circle's diameter fits round its
edge. It is written with the class name in front because it does not belong
to any particular number:

```sather
   wheel_edge(diameter : FLTD) : FLTD is
      return FLTD::pi * diameter;
   end;
```

## Angles are in radians

`.sin`, `.cos` and `.tan` take an angle, but not in degrees. They use
**radians**, where a half turn is π rather than 180. Giving them degrees is
not an error: it quietly gives the wrong answer.

Convert degrees to radians before calling them:

```sather
   ramp_rise(length, degrees : FLTD) : FLTD is
      radians ::= degrees * FLTD::pi / 180.0d;
      return length * radians.sin;
   end;
```

A ramp 10 metres long at 30 degrees rises `ramp_rise(10.0d, 30.0d)`, which is
`5.0`. Without the conversion, `30.0d.sin` treats 30 as radians — nearly five
whole turns — and answers `-0.988`.

## Finding an angle

`.atan2` goes the other way: given how far up and how far across, it answers
the angle. It is called on the *up* distance, with the *across* distance as
the argument:

```sather
   1.0d.atan2(1.0d)       -- 0.785398, which is π/4
```

The answer is in radians too. To get degrees, multiply by `180.0d` and divide
by `FLTD::pi`. One step up and one step across is 45 degrees.

## Powers of ten: exp10 and log10

`.exp10` is 10 to the power of the number:

```sather
   5.0d.exp10         -- 100000.0
   2.0d.exp10         -- 100.0
   1.0d.exp10         -- 10.0
   0.5d.exp10         -- 3.16228
   0.0d.exp10         -- 1.0
   (-3.0d).exp10      -- 0.001
```

`.log10` goes back the other way. It answers the question "10 to what power
gives this number?" That answer is the number's **logarithm**:

```sather
   100000.0d.log10    -- 5.0
   100.0d.log10       -- 2.0
   10.0d.log10        -- 1.0
   3.16228d.log10     -- 0.5
   1.0d.log10         -- 0.0
   0.001d.log10       -- -3.0
```

## exp and log

`.exp` and `.log` are the same pair, with *e* (about 2.718) in place of 10.
`.exp` raises *e* to a power, and `.log` answers "*e* to what power gives
this number?" Mathematicians use *e* for anything that grows or shrinks by the
same fraction each step: money earning interest, say, or a cup of tea
cooling:

```sather
   -- 80 degrees hotter than the room, the gap shrinking by 5% a minute
   tea_gap(minutes : FLTD) : FLTD is
      return 80.0d * (-0.05d * minutes).exp;
   end;
```

`.log` undoes `.exp`: `x.exp.log` is `x` again. That answers the question the
other way round — how long until the gap is down to 40 degrees?

```sather
   (80.0d / 40.0d).log / 0.05d      -- 13.8629 minutes
```
