# Hints

## 1. How many have we got?

- Ask `has_ind` first, and `raise` when the answer is false.
- The message is built with `+`, as any string is:
  `raise "Unknown prop: " + prop;`
- Nothing after a `raise` runs, so there is no `else` to write. The `return`
  below it is only reached when the prop is there.

## 2. Take one

- Call `count_of` for the number. If the prop is unknown, that call raises
  and `take_one` raises too — you do not have to write anything for it, and
  should not.
- Then check for nought and raise `"Out of " + prop`.
- Otherwise return one less.

## 3. Report back

- `protect` around a call to `take_one`, with a `when $STR then` arm.
- In the `protect` part, take one and build the success message from what
  it answered.
- In the `when` arm, the message is `exception.str` and nothing else. Do not
  try to work out which failure it was; whatever was raised is already the
  right words.
