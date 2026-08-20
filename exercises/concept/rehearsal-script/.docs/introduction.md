# String Builders

A `STR` never changes. So `+` cannot add to one — it has to make a whole new
string with the contents of both.

That is fine once. In a loop it is not:

```sather
   -- don't
   script ::= "";
   loop
      script := script + lines.elt!;
   end;
```

Every turn copies everything built so far into a new string and throws the
old one away. Ten lines means ten copies, each longer than the last. A
hundred lines means a hundred. The work grows with the *square* of the
number of lines, and a loop that looks harmless becomes the slow part of the
program.

## FSTR

`FSTR` is a string that *can* be changed — a **string builder**. Adding to
one usually just writes into space it already has, so a loop over a hundred
lines does about a hundred lines' worth of work rather than a hundred
copies.

```sather
   script ::= #FSTR;
   loop
      script := script + lines.elt!;
   end;
   return script.str;
```

Three things to notice.

**`#FSTR` makes an empty one.** `#FSTR(100)` makes one with room for a
hundred characters already set aside, which is worth doing when the size is
known.

**You must assign the result back.** `script := script + ...`, never
`script + ...` on its own. Usually the answer is the same builder that went
in, but when it has run out of room it is a bigger, new one — and dropping
the answer would leave you writing into the old one.

**`.str` at the end.** A routine promising `: STR` has to hand back a `STR`,
and `.str` makes one from the builder.

## What can be added

`+` on an `FSTR` accepts a string, a character, a whole number or a boolean,
so there is usually no need to convert first:

```sather
   line ::= #FSTR;
   line := line + 1 + ". " + "Enter" + '!';   -- "1. Enter!"
```

## New lines

`"\n"` inside a string is a new line — one character, written with two.

```sather
   script := script + "Enter" + "\n" + "Exit";
```
