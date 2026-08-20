# Classes with State

```sather
class SCOREBOARD is

   attr home_team, away_team : STR;
   attr home_score, away_score : INT;

   create(home, away : STR) : SAME is
      board ::= new;
      board.home_team := home;
      board.away_team := away;
      return board;
   end;

   home_goal is home_score := home_score + 1; end;

end; -- class SCOREBOARD
```

## attr, readonly attr, private attr

| Written | Read from outside | Changed from outside |
| --- | --- | --- |
| `attr x : INT` | yes | yes |
| `readonly attr x : INT` | yes | no |
| `private attr x : INT` | no | no |

`readonly` is the one to reach for by default. It lets anybody see the
score and insists that changing it goes through `home_goal`, which is where
the rules about scoring live.

## create and new

`new` produces an object of this class with every attribute empty. It may
only be used inside the class.

`create` is an ordinary routine with an agreed name: `#C(args)` is exactly
`C::create(args)`. A class may have several, told apart by their arguments,
and a class with none simply cannot be made with `#`.

## SAME

`SAME` stands for the class it is written in. In `create` it is the return
type; it also serves in an argument, and it is what makes an inherited
routine talk about the inheriting class rather than the one it came from.

## Routines with no return type

```sather
   home_goal is
      home_score := home_score + 1;
   end;
```

No `:` and no type. Such a routine is called as a statement and cannot
appear in an expression. It is the sign that the point of the call is the
change it makes.

## self

Inside a routine, `self` is the object it was called on. It is rarely
written, because an attribute or routine named on its own already means
`self`'s. It is needed when the object has to be passed on or returned:

```sather
   with_goal : SAME is
      home_score := home_score + 1;
      return self;
   end;
```

`self`, `new`, `void`, `result`, `value` and `out` are all words Sather has
taken, and none can be used as a name of your own.

## Reference, not value

An object is reached through a reference. Two names for the same scoreboard
see the same score:

```sather
   a ::= #SCOREBOARD("Vixens", "Magpies");
   b ::= a;         -- not a copy
   b.home_goal;
   a.home_score     -- 1
```

`immutable class`, later, is how to get the other behaviour.
