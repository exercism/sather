# Bits

An `INT` is 32 bits. Bit `0` is the lowest, worth 1; bit `i` is worth 2 to
the power `i`. The top bit, bit `31`, is the sign: when it is set the number
is negative.

A number used this way is a set of flags: each bit says yes or no to one
thing, and one number holds 32 of them.

## Binary literals

`0b` starts a number written in binary: `0b101` is `5`. Underscores may be
used to group digits.

## Reading and changing one bit

```sather
5.bit(0)              -- true:  5 is binary 101
5.bit(1)              -- false
5.set_bit(1)          -- 7:     bit 1 now set
7.unset_bit(1)        -- 5:     bit 1 now clear
5.set_bit(1, false)   -- 5:     set_bit with a BOOL sets or clears
```

These are built from the routines below. A mask with only bit `i` set is
`1.lshift(i)`.

| Wanted | Built from |
| --- | --- |
| is bit `i` set? | `x.band(1.lshift(i)) /= 0` |
| set bit `i` | `x.bor(1.lshift(i))` |
| clear bit `i` | `x.band(1.lshift(i).bnot)` |
| flip bit `i` | `x.bxor(1.lshift(i))` |

## Bitwise operations

| Routine | Each bit of the answer |
| --- | --- |
| `a.band(b)` | `1` where both are `1` |
| `a.bor(b)` | `1` where either is `1` |
| `a.bxor(b)` | `1` where exactly one is `1` |
| `a.bnot` | the opposite of `a`'s bit |

`a.bnot` is always `-a - 1`, so `0.bnot` is `-1`, the number with all 32
bits set.

Sather writes these as routines, not operators. There is no `&`, `|` or
`^`; `and`, `or` and `~` work only on `BOOL`.

## Shifts

| Routine | Moves bits | Fills in with |
| --- | --- | --- |
| `a.lshift(n)` | left | `0`s on the right |
| `a.rshift(n)` | right | copies of the sign bit on the left |
| `a.urshift(n)` | right | `0`s on the left |

`lshift(n)` multiplies by 2 to the power `n`, until bits fall off the top.
`rshift(n)` divides by it, and agrees with `/` even for negative numbers,
since both round down:

```sather
(-7).rshift(1)     -- -4
-7 / 2             -- -4
```

`urshift` treats the number as if it had no sign, so on a negative number
it gives a large positive answer: `(-1).urshift(28)` is `15`.

## Fields of bits

Several bits side by side can hold a small number. To read the field at
bits `4` to `7`, shift it down and keep the bottom four bits:

```sather
x.rshift(4).band(0b1111)
```

To write a value `v` into that field, clear the field, then put `v` in:

```sather
x.band(0b1111.lshift(4).bnot).bor(v.lshift(4))
```

## Counting bits

`bcount` answers how many bits are set: `0b1011.bcount` is `3`.
