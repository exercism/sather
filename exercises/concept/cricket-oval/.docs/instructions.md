# Instructions

The groundskeeper at a suburban cricket oval wants some help with the
numbers: how much rope the boundary needs, how far and in which direction a
shot went, and how far the ball rolls before the fielders get to it.

Every distance is in metres and every speed in metres per second. Positions
on the field are measured from the middle of the pitch: `x` metres straight
down the ground, and `y` metres across it, with left positive and right
negative.

All six tasks go in the `CRICKET_OVAL` class.

## 1. Rope for the boundary

The boundary is a circle round the middle of the pitch. Return the length of
rope it takes, which is 2 × π × the radius.

```sather
CRICKET_OVAL::boundary_length(70.0d)
-- => 439.823d
```

## 2. How far from the pitch?

Given a fielder's position, return how far they stand from the middle of the
pitch: the square root of x² + y².

```sather
CRICKET_OVAL::distance_from_pitch(30.0d, 40.0d)
-- => 50.0d
```

## 3. Which way did it go?

Given where a shot landed, return its direction in **degrees**: 0 is
straight down the ground, 90 is square on the left, -90 square on the right,
and 180 straight back past the keeper.

```sather
CRICKET_OVAL::shot_angle(50.0d, 50.0d)
-- => 45.0d
```

## 4. How far did it carry?

A ball hit at `speed`, rising at `angle` **degrees**, carries
speed² × sin(2 × angle) ÷ 9.8 metres before it first lands.

```sather
CRICKET_OVAL::carry(28.0d, 15.0d)
-- => 40.0d
```

## 5. Slowing on the grass

Rolling along the outfield, a ball loses speed: after `metres` its speed is
speed × e^(−0.02 × metres). Return the speed it has left.

```sather
CRICKET_OVAL::speed_after(30.0d, 50.0d)
-- => 11.0364d
```

## 6. Where will it stop being worth chasing?

Turn task 5 round. Given the speed a ball starts rolling at and a slower
`target` speed, return how many metres it rolls before it is down to the
target: ln(speed ÷ target) ÷ 0.02.

```sather
CRICKET_OVAL::metres_until(30.0d, 15.0d)
-- => 34.6574d
```
