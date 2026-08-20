# Instructions

The stage manager wants the rehearsal script typed up, and several parts of
it are built by repeating or joining things together.

All four tasks go in the `REHEARSAL_SCRIPT` class.

## 1. Repeat a cue

Given a cue and a number, return the cue that many times over, with nothing
between.

```sather
REHEARSAL_SCRIPT::repeat_cue("Ha", 3)
-- => "HaHaHa"
```

Repeating something no times gives the empty string.

## 2. The cast initials

Given the cast list, return the first letter of each name, run together.

```sather
REHEARSAL_SCRIPT::initials(|"Mia", "Ana", "Ben"|)
-- => "MAB"
```

## 3. Number the lines

Given the lines of a scene, number them from one, each on its own line.

```sather
REHEARSAL_SCRIPT::numbered_lines(|"Enter", "Exit"|)
-- => "1. Enter\n2. Exit"
```

There is a new line *between* the lines and none after the last. A scene
with no lines is the empty string.

## 4. Shout a line

Return a line with every letter turned into a capital.

```sather
REHEARSAL_SCRIPT::shout("quiet please")
-- => "QUIET PLEASE"
```
