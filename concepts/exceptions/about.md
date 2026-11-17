# Exceptions

```sather
   raise "Not on the menu: " + drink;
```

```sather
   protect
      ...
   when $STR then
      #OUT + exception.str;
   end;
```

## raise

`raise` takes any object. Raising a `STR` is the simple case and is what
this exercise uses. A class of your own carries more — which drink, for
which table — at the cost of somewhere to define it.

An exception travels outward through callers until a `protect` catches it.
If none does, the program stops and prints it.

Sather does not record which exceptions a routine may raise, and does not
make callers handle them. Nothing in the type of a routine says it can fail.

## protect

```sather
   protect
      body
   when $STR then
      ...
   when SOME_CLASS then
      ...
   end;
```

Arms are tried in order, and the first whose type matches the raised value
runs. `exception` is that value, and is only in scope inside an arm.

A `protect` with no matching arm does not catch: the exception carries on
outward as though the `protect` were not there.

## Where to catch

Catch where something can actually be done. A `protect` that swallows an
exception and carries on with a made-up value turns a loud failure into a
quiet wrong answer, which is worse.

```sather
   -- almost always wrong
   protect
      return risky;
   when $STR then
      return 0;
   end;
```

## Cleaning up

Sometimes a routine cannot handle an exception, but still has something to
do before it goes, such as closing a file. Sather has no `finally`. Instead,
an `else` arm does the cleaning up and then raises the same exception again:

```sather
   log ::= FILE::open_for_append("orders.txt");
   protect
      log + drink + ": " + price(drink) + "\n";    -- price may raise
   else
      log.close;
      raise exception;
   end;
   log.close;
```

An `else` arm catches an exception of any type, and `raise exception` passes
it on unchanged, so the caller sees exactly what was raised. The cleaning up
is written twice: once in `else` for when something was raised, and once
after `end` for when nothing was.

Cleaning up does not undo anything. The line is written from left to right,
so if `tea` is not on the menu, the file is left ending in `tea: ` with no
price after it.

A `return` inside the `protect` part skips the cleaning up after `end`, so
keep returns out of it. And only what is raised with `raise` reaches `else`.
An index out of bounds or a broken contract stops the program straight
away, and nothing is cleaned up.

## Exceptions or contracts?

Both concern things going wrong, and they are for opposite cases.

An **exception** is for something that can genuinely happen and that the
caller may reasonably not have been able to prevent — a drink that is not
on the menu, a file that is not there.

A **contract**, taught in Safety Harness, is for something that must never
happen — a caller passing a negative weight — and is a statement that the
caller has a bug. Contracts are checked only when asked for, and a violated
one stops the program rather than raising something catchable.

Roughly: if a careful caller could still hit it, raise. If hitting it means
the caller is wrong, put it in a contract.
