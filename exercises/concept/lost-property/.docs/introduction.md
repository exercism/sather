# Generic Classes

You have used `ARRAY{STR}`, `FMAP{STR,INT}` and `FSET{STR}` since early on.
The braces have always held a type. Now you write a class with braces of its
own.

## The problem

A collector keeps things in matched pairs: two coins from the same mint, two
stamps from the same sheet. A pair of coins:

```sather
class COIN_PAIR is
   attr left, right : COIN;
   ...
end;
```

and then the same class again for stamps, and again for banknotes. Three
copies that differ in one word.

## The type parameter

```sather
class PAIR{T} is

   attr left, right : T;

   create(a, b : T) : SAME is
      pair ::= new;
      pair.left := a;
      pair.right := b;
      return pair;
   end;

end; -- class PAIR{T}
```

`{T}` after the class name is a **type parameter**. `T` is not a type — it
is a stand-in for whatever type is supplied when the class is used. Inside
the class, `T` is used exactly as any type name would be.

## Using it

Supply the type in braces:

```sather
   stamps ::= #PAIR{STR}("Penny Black", "Penny Red");
   years ::= #PAIR{INT}(1840, 1841);

   stamps.left      -- "Penny Black", a STR
   years.right      -- 1841, an INT
```

`PAIR{STR}` and `PAIR{INT}` are two different types. Putting one
where the other is wanted is an error the compiler catches, exactly as if
you had written the two classes out by hand — which, in effect, is what
happens: Sather builds a separate class from the pattern for each type
actually used.

So there is no cost to this at run time, and no loss of type information:
`stamps.left` really is a `STR`, not something that has to be checked or
converted.

## More than one

A class may take several parameters, separated by commas. `FMAP{K,T}` is the
example you already know.

```sather
class CATALOGUED{N,T} is
   attr number : N;
   attr piece : T;
   ...
end;
```

## Naming

Single capital letters by convention: `T` for a thing, `K` for a key, `E`
for an element. The library uses them throughout.
