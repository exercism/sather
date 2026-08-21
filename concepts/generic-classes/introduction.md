# Generic Classes

You have used `ARRAY{STR}`, `FMAP{STR,INT}` and `FSET{STR}` since early on.
The braces have always held a type. Now you write a class with braces of its
own.

## The problem

The lost property office needs a box that holds one thing and remembers who
handed it in. A box for a jumper:

```sather
class JUMPER_BOX is
   attr item : JUMPER;
   ...
end;
```

and then the same class again for a water bottle, and again for a phone.
Three copies that differ in one word.

## The type parameter

```sather
class LOST_BOX{T} is

   attr item : T;

   create(thing : T) : SAME is
      box ::= new;
      box.item := thing;
      return box;
   end;

end; -- class LOST_BOX{T}
```

`{T}` after the class name is a **type parameter**. `T` is not a type — it
is a stand-in for whatever type is supplied when the class is used. Inside
the class, `T` is used exactly as any type name would be.

## Using it

Supply the type in braces:

```sather
   jumper ::= #LOST_BOX{STR}("blue jumper");
   count ::= #LOST_BOX{INT}(3);

   jumper.item      -- "blue jumper", a STR
   count.item       -- 3, an INT
```

`LOST_BOX{STR}` and `LOST_BOX{INT}` are two different types. Putting one
where the other is wanted is an error the compiler catches, exactly as if
you had written the two classes out by hand — which, in effect, is what
happens: Sather builds a separate class from the pattern for each type
actually used.

So there is no cost to this at run time, and no loss of type information:
`jumper.item` really is a `STR`, not something that has to be checked or
converted.

## More than one

A class may take several parameters, separated by commas. `FMAP{K,T}` is the
example you already know.

```sather
class LABELLED{L,T} is
   attr label : L;
   attr item : T;
   ...
end;
```

## Naming

Single capital letters by convention: `T` for a thing, `K` for a key, `E`
for an element. The library uses them throughout.
