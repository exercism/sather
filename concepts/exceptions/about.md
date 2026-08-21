# Exceptions

```sather
   raise "Unknown prop: " + prop;
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
this exercise uses. A class of your own carries more — which prop, how many
were wanted — at the cost of somewhere to define it.

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

## Exceptions or contracts?

Both concern things going wrong, and they are for opposite cases.

An **exception** is for something that can genuinely happen and that the
caller may reasonably not have been able to prevent — a prop missing from
the table, a file that is not there.

A **contract**, which is the next exercise, is for something that must never
happen — a caller passing a negative weight — and is a statement that the
caller has a bug. Contracts are checked only when asked for, and a violated
one stops the program rather than raising something catchable.

Roughly: if a careful caller could still hit it, raise. If hitting it means
the caller is wrong, put it in a contract.
