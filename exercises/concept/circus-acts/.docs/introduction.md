# Abstract Classes

A circus show is a list of acts. Juggling, trapeze and tumbling are
different things with different insides, but the person building the running
order only needs two things from each: what it is called, and how long it
takes.

An **abstract class** describes that much and no more.

```sather
abstract class $ACT is
   name : STR;
   minutes : INT;
end; -- abstract class $ACT
```

Its name starts with `$`. It lists routines with no bodies: signatures only,
each ending at the semicolon. Nothing can be made from it — there is no
`create` and no `new`.

## Conforming

A real class promises to be an `$ACT` by naming it after `<`:

```sather
class JUGGLING < $ACT is

   create : SAME is return new; end;

   name : STR is return "Juggling"; end;

   minutes : INT is return 5; end;

end; -- class JUGGLING
```

`<` is read "is a". The class must supply every routine the abstract class
lists, with the same arguments and the same return type. Leaving one out is
a compile error, not a surprise at run time.

A class may add whatever else it likes. `TRAPEZE` can hold a height that no
other act has; the abstract class neither knows nor cares.

## Using the type

`$ACT` is a type, so anything can be declared with it:

```sather
   acts : ARRAY{$ACT} := |#JUGGLING, #TRAPEZE(4), #TUMBLING|;
```

That array holds objects of three different classes at once, which an
`ARRAY{JUGGLING}` could not.

## Dispatch

```sather
   loop
      total := total + acts.elt!.minutes;
   end;
```

`acts.elt!` is an `$ACT`. Which `minutes` runs is decided when the line runs,
by what the object actually is: `JUGGLING::minutes` for the juggling,
`TRAPEZE::minutes` for the trapeze. That choosing is called **dispatch**.

The routine doing the adding never asks what kind of act it has. Adding a
fourth kind of act means writing one new class and changing nothing else —
which is the whole reason to do it this way.
