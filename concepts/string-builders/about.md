# String Builders

`STR` is immutable; `FSTR` is not. Use `STR` for text that is finished and
`FSTR` for text still being assembled.

```sather
   b ::= #FSTR;              -- empty
   b ::= #FSTR(256);         -- empty, with room for 256 characters
   b ::= #FSTR("Act I: ");   -- starting from a string
   b := b + "Enter";
   s ::= b.str;              -- a STR again
```

## Always assign the result back

```sather
   b := b + "Enter";         -- yes
   b + "Enter";              -- no: the answer is thrown away
```

`FSTR` grows by **amortised doubling**: when it runs out of room it takes a
new, larger array — twice the size — and copies into that. So the answer is
usually the same object, and occasionally a different one. Writing
`b := b + x` every time is correct in both cases, and is the only spelling
worth learning.

Doubling is what makes the total work proportional to the length rather than
its square: the copies get rarer as fast as they get more expensive.

## Why not just use `+` on STR?

Joining a fixed, small number of pieces with `+` is clear and fine:

```sather
   return piece + " by " + composer;
```

The problem is only a loop, where the number of joins is not known when the
code is written. A rough guide: if the `+` is inside a `loop`, reach for
`FSTR`.

## Useful routines

| Call | Does |
| --- | --- |
| `b + x` | appends; `x` may be `STR`, `CHAR`, `INT`, `BOOL` … |
| `b.size` | how many characters so far |
| `b.str` | a finished `STR` |
| `b.clear` | empties it, keeping the space |

## Escapes

| Written | Is |
| --- | --- |
| `"\n"` | a new line |
| `"\t"` | a tab |
| `"\""` | a double quote |
| `"\\"` | a backslash |
