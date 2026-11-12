# Classes with State

Every class so far has been a box of routines. Each one took its arguments,
worked out an answer and forgot everything.

A class can instead **remember** things. A vending machine has to: whether
it hands over a snack depends on every coin put in since the last sale.

## Attributes

`attr` gives a class something to remember.

```sather
class VENDING_MACHINE is

   attr item : STR;
   attr price : INT;
   attr credit : INT;

end; -- class VENDING_MACHINE
```

Each `attr` becomes a routine that reads the value, and one that changes it:

```sather
   machine.credit              -- read it
   machine.credit := 200;      -- change it
```

Attributes of the same type can share a declaration, as arguments can:

```sather
   attr price, credit : INT;
```

## Objects

A class with attributes is a pattern for making **objects**. Each object has
its own copies of the attributes, so two machines hold two credits.

`new` makes an object. It goes inside a routine called `create`, which then
fills the object in and hands it back:

```sather
   create(snack : STR, cents : INT) : SAME is
      machine ::= new;
      machine.item := snack;
      machine.price := cents;
      return machine;
   end;
```

`SAME` means "this class". Writing `VENDING_MACHINE` there would say the
same thing, but `SAME` keeps working if the class is renamed.

## Making one

`#` calls `create`:

```sather
   machine ::= #VENDING_MACHINE("Crisps", 250);
```

You have been using `#` since `rehearsal-script` — `#FSTR` is exactly this.

## Routines that change the object

Inside the class, an attribute is used by name, with no object in front. It
means the object the routine was called on.

```sather
   insert(cents : INT) is
      credit := credit + cents;
   end;
```

`insert` declares no return type, because it answers nothing — it changes
the object instead. Call it as a statement:

```sather
   machine.insert(200);
```

## Attributes start empty

An attribute nobody has set holds nought for an `INT`, `false` for a `BOOL`,
and void for a string or object. So a new machine holds no credit without
anything having to say so.
