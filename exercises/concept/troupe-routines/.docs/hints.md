# Hints

## General

- An `include` goes inside the class, usually as its first line.
- Only what you rename or leave out changes. Everything else comes in as it
  was.

## 1. The jazz routine

- One `include` inside the class, with nothing renamed and nothing left
  out.
- Nothing else. The class body is that line and no more.

## 2. The tap routine

- One entry in the include: `describe` renamed to nothing.
- The `-> ;` with nothing after the arrow leaves `describe` out, which is
  what makes room for the one you write.
- This compiler would let your own `describe` win without it, silently.
  The `-> ;` says out loud that the included one is being replaced, and the
  task asks for it.

## 3. The finale

- Two entries in one include, separated by a comma: one renaming `counts`
  to its new name, one leaving `describe` out.
- Then write your own `counts`, built from the renamed one, and your own
  `describe`.
- `describe` should call `counts`, not work the number out again.
- Remember that a number cannot have a string added to it. A description
  that starts with a string is fine, because a string will take a number
  added on; one that starts with a number needs `.str` first.
