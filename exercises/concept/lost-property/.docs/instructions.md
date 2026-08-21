# Instructions

The school lost property office keeps everything in boxes, and what goes in
a box could be anything: a jumper, a number of things, a name.

Write a `LOST_BOX{T}` class. The stub gives you the class header.

## 1. Take something in

`create` takes the thing and the name of whoever handed it in, and gives a
box. A box starts unclaimed.

```sather
box ::= #LOST_BOX{STR}("blue jumper", "Mia");
box.item
-- => "blue jumper"
box.handed_in_by
-- => "Mia"
box.claimed
-- => false
```

## 2. Claim it

`claim` marks the box as claimed. It answers nothing.

```sather
box.claim;
box.claimed
-- => true
```

## 3. Is it still waiting?

`waiting` answers whether the box has not been claimed.

```sather
box.waiting
-- => false
```

## 4. Swap the contents

`replace` takes a new thing, puts it in the box and answers what was there
before. The thing going in and the thing coming out are both `T`.

```sather
old ::= box.replace("red jumper");
old
-- => "blue jumper"
box.item
-- => "red jumper"
```

## 5. Write it up

`describe` answers a line about the box, like
`"blue jumper, handed in by Mia"`.

To put the item into a string, the class needs to know that a `T` can be
turned into one. Constrain the parameter: write the class header as
`class LOST_BOX{T < $STR}`, and then `item.str` is allowed.

```sather
box.describe
-- => "blue jumper, handed in by Mia"
```
