# Instructions

You are running the lighting desk for the school play. The desk keeps the
whole rig in one `INT`: light `0` is bit `0`, light `1` is bit `1`, and so
on. A bit that is `1` means that light is on.

All six tasks go in the `LIGHTING_DESK` class.

## 1. Is this light on?

Given the rig and a light number, say whether that light is on.

```sather
LIGHTING_DESK::is_on(5, 2)
-- => true
```

## 2. One light on its own

The stage manager often wants a rig with exactly one light on and every
other light off. Given the light number, give that rig.

```sather
LIGHTING_DESK::only(3)
-- => 8
```

## 3. Switch a light on

Give the rig with this light switched on. Every other light stays as it
was, and a light that is already on stays on.

```sather
LIGHTING_DESK::switch_on(5, 1)
-- => 7
```

## 4. Switch a light off

Give the rig with this light switched off. Every other light stays as it
was, and a light that is already off stays off.

```sather
LIGHTING_DESK::switch_off(7, 1)
-- => 5
```

## 5. Flip a light

Give the rig with this one light changed: on if it was off, off if it was
on. Every other light stays as it was.

```sather
LIGHTING_DESK::flip(5, 1)
-- => 7
```

## 6. The back row

Lights `0` to `7` hang over the front of the stage and lights `8` to `15`
over the back. Lights `16` and above are in the foyer and belong to neither
row.

The back row has its own little panel, which numbers its lights `0` to `7`.
Give the rig as that panel sees it: light `8` becomes light `0`, light `9`
becomes light `1`, and so on, with nothing else on.

```sather
LIGHTING_DESK::back_row(768)
-- => 3
```

`768` is `512 + 256`: lights `9` and `8`, which the back panel calls `1`
and `0`.
