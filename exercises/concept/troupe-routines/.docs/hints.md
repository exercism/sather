# Hints

## General

- An `include` goes inside the class, usually as its first line.
- Only what you rename or leave out changes. Everything else comes in as it
  was.

## 1. The jazz routine

- One line inside the class: `include WARM_UP;`
- Nothing else. The class body is that line and no more.

## 2. The tap routine

- `include WARM_UP describe -> ;`
- The `-> ;` with nothing after the arrow leaves `describe` out, which is
  what makes room for the one you write.
- Without it, the compiler complains that `describe` is defined twice. That
  error is the feature: Sather will not silently pick one.

## 3. The finale

- Two entries in one include, separated by a comma:
  `include WARM_UP counts -> warm_up_counts, describe -> ;`
- Then write `counts` returning `warm_up_counts * 2`, and `describe`.
- `describe` should call `counts`, not work the number out again.
- Remember that a number cannot have a string added to it, so a description
  starting with words is fine: `"Finale: " + counts + " counts"`.
