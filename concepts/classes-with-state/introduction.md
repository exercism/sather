# Classes with State

Every class so far has been a box of routines. Each one took its arguments,
worked out an answer and forgot everything.

A class can instead **remember** things. A scoreboard has to: the score now
depends on every goal since the game started.

## Attributes

`attr` gives a class something to remember.

```sather
class SCOREBOARD is

   attr home_score : INT;
   attr away_score : INT;

end; -- class SCOREBOARD
```

Each `attr` becomes a routine that reads the value, and one that changes it:

```sather
   board.home_score            -- read it
   board.home_score := 4;      -- change it
```

Attributes of the same type can share a declaration, as arguments can:

```sather
   attr home_score, away_score : INT;
```

## Objects

A class with attributes is a pattern for making **objects**. Each object has
its own copies of the attributes, so two scoreboards keep two scores.

`new` makes an object. It goes inside a routine called `create`, which then
fills the object in and hands it back:

```sather
   create(home, away : STR) : SAME is
      board ::= new;
      board.home_team := home;
      board.away_team := away;
      return board;
   end;
```

`SAME` means "this class". Writing `SCOREBOARD` there would say the same
thing, but `SAME` keeps working if the class is renamed.

## Making one

`#` calls `create`:

```sather
   board ::= #SCOREBOARD("Vixens", "Magpies");
```

You have been using `#` since `rehearsal-script` — `#FSTR` is exactly this.

## Routines that change the object

Inside the class, an attribute is used by name, with no object in front. It
means the object the routine was called on.

```sather
   home_goal is
      home_score := home_score + 1;
   end;
```

`home_goal` declares no return type, because it answers nothing — it changes
the object instead. Call it as a statement:

```sather
   board.home_goal;
```

## Attributes start empty

An attribute nobody has set holds nought for an `INT`, `false` for a `BOOL`,
and void for a string or object. So a new scoreboard reads 0 to 0 without
anything having to say so.
