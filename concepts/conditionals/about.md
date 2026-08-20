# Conditionals

```sather
   if score >= 5 then
      return "Recalled";
   else
      return "Thank you";
   end;
```

The question between `if` and `then` must be a `BOOL`. Sather will not
accept a number there, so there is no C-style habit of treating zero as
false.

## The shape

```sather
   if first_question then
      ...
   elsif second_question then
      ...
   elsif third_question then
      ...
   else
      ...
   end;
```

Questions are asked from the top down, and the first one that answers true
wins. Everything below it is skipped without being asked. That is why a
chain must go from the most specific test to the least: putting
`score >= 5` above `score >= 8` means the second is never reached.

`else` is optional. `elsif` may be repeated as often as needed.

## Conditionals are statements, not values

`if` does not itself produce a value, so this is not Sather:

```sather
   -- wrong
   grade := if score > 5 then "pass" else "fail" end;
```

Either return from inside each branch, or assign to a variable inside each
branch.

## When not to use one

A routine that answers a question should return the question:

```sather
   -- say this
   old_enough(age : INT) : BOOL is
      return age >= 13;
   end;

   -- not this
   old_enough(age : INT) : BOOL is
      if age >= 13 then return true; else return false; end;
   end;
```

The second says nothing the first does not, at three times the length.

## Nesting

An `if` may hold another `if`. Often it does not need to: two questions that
both have to hold can be joined with `and` instead, which reads better.

```sather
   if score >= 8 and sings then
      return "Lead";
   end;
```
