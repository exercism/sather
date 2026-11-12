# String Builders

A `STR` never changes. So `+` cannot add to one — it has to make a whole new
string with the contents of both.

That is fine once. In a loop it is not:

```sather
   -- don't
   log ::= "";
   loop
      port ::= ports.elt!;
      log := log + "Called at " + port + "\n";
   end;
```

Every turn copies everything built so far into a new string and throws the
old one away. Ten ports means ten copies, each longer than the last. A
hundred ports means a hundred. The work grows with the *square* of the
number of ports, and a loop that looks harmless becomes the slow part of the
program.

## FSTR

`FSTR` is a string that *can* be changed — a **string builder**. Adding to
one usually just writes into space it already has, so a loop over a hundred
ports does about a hundred ports' worth of work rather than a hundred
copies.

```sather
   log ::= #FSTR;
   loop
      port ::= ports.elt!;
      log := log + "Called at " + port + "\n";
   end;
   return log.str;
```

Four things to notice.

**`#FSTR` makes an empty one.** `#FSTR(100)` makes one with room for a
hundred characters already set aside, which is worth doing when the size is
known.

**You must assign the result back.** `log := log + ...`, never
`log + ...` on its own. Usually the answer is the same builder that went
in, but when it has run out of room it is a bigger, new one — and dropping
the answer would leave you writing into the old one.

**Take from an iterator before you add.** Each `port` above comes out of
`ports.elt!` on a line of its own. Written as one line,
`log := log + "Called at " + ports.elt! + "\n"`, the last turn adds
`"Called at "` to the builder and only then finds no port left. The loop
ends, and the assignment back never happens. If the builder had room, it
keeps a stray `Called at ` on the end. If it had to grow, `log` is left
naming the old builder, which `+` has already thrown away, and the next use
of `log` stops the program with "Attr access of destroyed object".

**`.str` at the end.** A routine promising `: STR` has to hand back a `STR`,
and `.str` makes one from the builder.

## What can be added

`+` on an `FSTR` accepts a string, a character, a whole number or a boolean,
so there is usually no need to convert first:

```sather
   entry ::= #FSTR;
   entry := entry + "Day " + 3 + ": " + "fog" + '!';   -- "Day 3: fog!"
```

## New lines

`"\n"` inside a string is a new line — one character, written with two.

```sather
   log := log + "Dover" + "\n" + "Calais";
```
