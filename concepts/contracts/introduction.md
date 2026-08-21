# Contracts

A routine's arguments and return type say what *kind* of thing goes in and
comes out. They cannot say that a weight must be positive, or that a harness
never reports more spare capacity than it has.

A **contract** says those things, in the routine's own header, where anybody
reading it will see them.

## pre

`pre` states what must be true when the routine is called. It goes between
the return type and the `is`.

```sather
   spare_capacity(load : INT) : INT
      pre load >= 0
   is
      return limit - load;
   end;
```

That is a demand on the **caller**: do not call this with a negative load.

## post

`post` states what will be true when the routine answers. Inside it,
`result` is the value being returned.

```sather
   percent_used(load : INT) : INT
      pre load >= 0
      post result >= 0
   is
      return load * 100 / limit;
   end;
```

That is a promise to the caller. A routine with both is a bargain: give me
this, and I will give you that.

Several conditions join with `and`, as any booleans do:

```sather
      pre load >= 0 and load <= limit
```

## Contracts are not exceptions

A raised exception is for something that can happen. A broken contract means
a **bug** — somebody called the routine wrongly, or the routine did not do
what it said.

So a broken contract does not raise something catchable. When contract
checking is switched on, the program stops and prints which routine, and
which condition. When it is switched off, the condition is not even tested,
and the program runs on into whatever nonsense follows.

That is why a contract is a statement about correctness rather than a way of
handling bad input. If bad input is expected, check it and `raise`. If bad
input means the caller is broken, say so with `pre`.

## Switching checking on

This Sather checks contracts when the compiler is given `-chk`:

```
sacomp -chk mine.sa -main MAIN -o mine
```

Without it, `pre` and `post` are documentation the compiler has read and
agreed is well-formed, and nothing more. The tests for this exercise are
built without `-chk`, so they cannot catch a broken contract for you; they
check that the routines do the right thing when used properly.
