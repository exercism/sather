# Iterators

An iterator is a routine whose name ends in `!` and which may only be called
inside a `loop`. Each time round the loop it produces its next value; when
it runs out, the loop ends at once.

```sather
   loop
      crop ::= crops.elt!;
      #OUT + "Sow " + crop + "\n";
   end;
```

Take the value into a variable first, as here. An iterator that runs out
ends the loop part way through its line, and anything earlier on that line
has already happened: `#OUT + "Sow " + crops.elt!` prints a stray `Sow ` on
the last turn.

Sather has no `for` statement. This is what replaces it, and it is the
feature the language is known for.

## The ones worth knowing early

| Iterator | Gives |
| --- | --- |
| `a.elt!` | each element of `a`, in order |
| `a.ind!` | each position of `a`: 0, 1, 2 … |
| `n.upto!(m)` | `n`, `n+1` … `m` |
| `n.downto!(m)` | `n`, `n-1` … `m` |
| `n.times!` | runs `n` times, giving nothing |
| `n.up!` | `n`, `n+1`, … and never ends |
| `s.elt!` | each character of a string |

`until!`, `while!` and `break!` are iterators too. That is why they end in
`!` and why they only work inside a loop.

## Where the call goes

An iterator call may appear anywhere an expression may, including in the
middle of a condition:

```sather
   loop
      if crops.elt! = "rhubarb" then #OUT + "Mind the leaves\n"; end;
   end;
```

Each *place* in the program where an iterator is written keeps its own
position. Writing `crops.elt!` twice in one loop body makes two independent
walks of the array, which is almost never what is wanted:

```sather
   loop
      #OUT + crops.elt! + " and " + crops.elt!;   -- two separate walks
   end;
```

Ask once and put the value in a variable instead.

## Ending the loop

The loop ends as soon as *any* iterator in it runs out — not when all of
them do. With one iterator that is obvious. With several it is the rule that
catches everybody, and it is what the next exercise is about.

## Which to reach for

Prefer `elt!` when the values are wanted and `ind!` when the positions are.
Fall back to `upto!` over `0 .. a.size - 1` only when both are needed at
once, or when the answer is a position rather than a value.
