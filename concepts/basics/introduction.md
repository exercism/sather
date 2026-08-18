# Basics

A Sather program is made of **classes**. A class is a named box that holds
routines. A **routine** is a named piece of work that produces an answer.

```sather
class GREETER is

   hello : STR is
      return "Hello!";
   end;

end; -- class GREETER
```

Reading that from the top:

- `class GREETER is` opens the box and names it. Class names are written in
  capitals.
- `hello : STR is` starts a routine called `hello` that produces a `STR` — a
  piece of text, called a *string*. The `: STR` is a promise about what kind
  of answer comes back.
- `return "Hello!";` hands back the answer. Text is written between double
  quotes.
- `end;` closes the routine, and the second `end;` closes the class.

Everything after `--` on a line is a **comment**. Sather ignores it; it is
there for people.

```sather
-- This line is for the reader, not the computer.
```

To use a routine from somewhere else, write the class name, two colons, and
the routine name:

```sather
GREETER::hello        -- this is "Hello!"
```

Inside the same class you can leave the class name off:

```sather
class GREETER is

   hello : STR is
      return "Hello!";
   end;

   greeting_again : STR is
      return hello;      -- calls the routine just above
   end;

end; -- class GREETER
```

A routine that takes no arguments is called without brackets — `hello`, not
`hello()`.
