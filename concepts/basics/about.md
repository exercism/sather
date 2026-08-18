# Basics

A Sather program is made of **classes** that hold **routines**.

```sather
class GREETER is

   hello : STR is
      return "Hello!";
   end;

end; -- class GREETER
```

## Classes

A class is named in capitals, with underscores between words:
`GREETER`, `STAGE_DIRECTIONS`. The name of the file usually matches, in lower
case: `stage_directions.sa`.

Every routine lives inside a class. There is no code outside one.

## Routines

A routine that produces an answer declares the kind of answer after a colon:

```sather
   hello : STR is
      return "Hello!";
   end;
```

`STR` is the type for text. A routine that takes no arguments is written and
called without brackets.

A routine can take arguments, written in brackets after the name:

```sather
   louder(word : STR) : STR is
      return word;
   end;
```

`return` hands an answer back and stops the routine right away, so any lines
below it are skipped.

## Calling

From outside the class, name the class, then `::`, then the routine:

```sather
GREETER::hello
```

From inside the same class, the class name can be left off. This is the usual
way to let one routine use another:

```sather
   greeting_again : STR is
      return hello;
   end;
```

## Comments

Two dashes begin a comment that runs to the end of the line.

```sather
   -- Explain why, not what: the code already says what.
   hello : STR is
      return "Hello!";   -- a trailing comment is fine too
   end;
```

By convention a class ends with a comment naming it. Routines, loops and
classes all close with `end;`, so the comment says which one this `end;`
belongs to:

```sather
end; -- class GREETER
```

## Semicolons

Statements end with a semicolon. The semicolon after the last statement in a
routine is optional, but writing it every time is one less thing to think
about.
