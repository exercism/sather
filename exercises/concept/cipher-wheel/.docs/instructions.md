# Instructions

A cipher wheel is two discs, one inside the other, that turns the alphabet
round: set it to 3 and every letter becomes the one three places along, with
`z` coming back round to `a`. Detectives have used them for centuries. You
are building one.

All five tasks go in the `CIPHER_WHEEL` class.

## 1. Is it a letter?

```sather
CIPHER_WHEEL::is_letter('m')
-- => true
CIPHER_WHEEL::is_letter('7')
-- => false
```

## 2. Shout it

Return the capital of a character. Anything that is not a letter comes back
unchanged.

```sather
CIPHER_WHEEL::shout('m')
-- => 'M'
```

## 3. What number is it?

Return the number that stands for a character.

```sather
CIPHER_WHEEL::code('a')
-- => 97
```

## 4. The first character

Return the first character of a string.

```sather
CIPHER_WHEEL::first_character("Marlowe")
-- => 'M'
```

## 5. Turn the wheel

Given a small letter and a number of places, return the letter that many
places along the alphabet. Past `z` it comes back round to `a`.

```sather
CIPHER_WHEEL::turn('a', 3)
-- => 'd'
CIPHER_WHEEL::turn('z', 1)
-- => 'a'
```

Turning backwards works too, with a negative number of places.

```sather
CIPHER_WHEEL::turn('a', -1)
-- => 'z'
```

You may assume the character handed in is a small letter.
