# Conditionals

A **conditional** picks between two courses of action depending on whether
something is true.

```sather
   verdict(score : INT) : STR is
      if score >= 5 then
         return "Recalled";
      else
         return "Thank you";
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
   verdict(score : INT) : STR is
      if score >= 8 then
         return "Cast";
      elsif score >= 5 then
         return "Recalled";
      else
         return "Thank you";
      end;
   end;
```

The order matters. A score of `9` is caught by the first question and never
reaches the second, even though `9 >= 5` is also true. Writing the tests in
the wrong order is the usual way to get this wrong.

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
