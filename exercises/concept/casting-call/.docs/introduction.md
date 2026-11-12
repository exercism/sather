# Conditionals

A **conditional** picks between two courses of action depending on whether
something is true.

```sather
   kettle(celsius : INT) : STR is
      if celsius >= 100 then
         return "Boiling";
      else
         return "Not yet";
      end;
   end;
```

Reading that: `if`, then a question that answers `true` or `false`, then
`then`. The lines after `then` run when the answer is true, and the lines
after `else` run when it is false. `end;` closes the whole thing.

## More than two ways

`elsif` adds another question, asked only when the ones above it came out
false.

```sather
   postage(grams : INT) : INT is
      if grams <= 100 then
         return 120;
      elsif grams <= 500 then
         return 300;
      else
         return 750;
      end;
   end;
```

The order matters. A 50 gram letter is caught by the first question and never
reaches the second, even though `50 <= 500` is also true. Swap the two
questions and every parcel up to 500 grams is charged 300, letters included.
Asking the questions in the wrong order is the usual way to get this wrong.

It is spelled `elsif` — not `elseif`, and not `else if`.

## Leaving out the else

`else` may be left off when there is nothing to do in that case.

```sather
   if late then
      apologise;
   end;
```

A routine that must return something needs every path to return, so in this
exercise every `if` keeps its `else`.
