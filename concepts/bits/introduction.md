# Bits

Inside the computer an `INT` is stored in binary, as a row of **bits**,
each a `1` or a `0`. Counting from nought at the right-hand end, bit `0`
stands for 1, bit `1` for 2, bit `2` for 4, bit `3` for 8, and so on, each
worth twice the one before. `5` is `4 + 1`, so it is `101` in binary: bits
`2` and `0` are set and bit `1` is not.

This is how a single number can carry several yes-or-no facts at once, one
per bit.

## Reading one bit

`.bit(i)` asks whether bit `i` is set, and answers `true` or `false`:

```sather
5.bit(0)     -- true
5.bit(1)     -- false
5.bit(2)     -- true
12.bit(3)    -- true, because 12 is 8 + 4
```

## Writing numbers in binary

A number starting `0b` is written in binary, which makes the bits easy to
see. `0b101` is just another way to write `5`.

## Combining two numbers bit by bit

These routines line two numbers up and work out each bit of the answer from
the two bits in the same place.

| Routine | A bit of the answer is `1` when |
| --- | --- |
| `band` | the bit is `1` in **both** numbers |
| `bor` | the bit is `1` in **either** number, or both |
| `bxor` | the bit is `1` in **exactly one** of them |

```sather
0b1100.band(0b1010)     -- 0b1000, which is 8
0b1100.bor(0b1010)      -- 0b1110, which is 14
0b1100.bxor(0b1010)     -- 0b0110, which is 6
```

They are the same idea as `and`, `or` and "one but not the other" on
`BOOL`s, done to every bit at once.

`bnot` takes no argument and turns every bit over: each `1` becomes `0` and
each `0` becomes `1`.

```sather
0b1100.bnot.band(0b1111)     -- 0b0011, which is 3
```

`bnot` on its own gives a negative number, because it also turns over all
the `0` bits to the left that you normally never think about. Combined
with `band`, as here, that does not matter.

## Shifting

`lshift(n)` moves every bit `n` places to the left, filling in with `0`s on
the right. Each place left doubles the number.

```sather
3.lshift(2)      -- 0b11 becomes 0b1100, which is 12
1.lshift(5)      -- 32: bit 5 and nothing else
```

`rshift(n)` moves every bit `n` places to the right. Bits that fall off the
right-hand end are gone. Each place right halves the number, throwing away
any remainder, just like `/ 2`.

```sather
0b110110.rshift(1)     -- 0b11011, which is 27
0b110110.rshift(3)     -- 0b110, which is 6
```

`urshift(n)` also shifts right. The two differ only for negative numbers:
`rshift` keeps a negative number negative, while `urshift` always fills in
with `0`s on the left, so a negative number becomes a large positive one.

```sather
(-8).rshift(1)      -- -4
(-8).urshift(1)     -- 2147483644
```

For numbers that are not negative, `rshift` and `urshift` give the same
answer.
