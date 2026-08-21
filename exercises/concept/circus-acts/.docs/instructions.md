# Instructions

A circus show is a running order of acts. Different acts have completely
different insides, and whoever assembles the show needs the same two things
from each of them.

This is the first exercise where you write several classes in one file. The
stub gives you the abstract class; write the rest below it.

## 1. The three acts

Write three classes, each an `$ACT`.

| Class | `name` | `minutes` |
| --- | --- | --- |
| `JUGGLING` | `"Juggling"` | 5 |
| `TUMBLING` | `"Tumbling"` | 3 |
| `TRAPEZE` | `"Trapeze at "` then the height then `"m"` | 8 |

`JUGGLING` and `TUMBLING` are made with no arguments. `TRAPEZE` is made with
the height in metres:

```sather
#JUGGLING
#TRAPEZE(4)
```

so `#TRAPEZE(4).name` is `"Trapeze at 4m"`.

## 2. The show

Write a `CIRCUS_ACTS` class with three routines, each taking the running
order as an `ARRAY{$ACT}`.

**`total_minutes`** — how long the whole show takes.

```sather
CIRCUS_ACTS::total_minutes(|#JUGGLING, #TUMBLING|)
-- => 8
```

**`billing`** — the names of the acts, joined with `", "`.

```sather
CIRCUS_ACTS::billing(|#JUGGLING, #TUMBLING|)
-- => "Juggling, Tumbling"
```

**`longest`** — the name of the act that takes longest. Where two are equal,
the earlier one wins. An empty show has no longest act, so the answer is
`""`.

```sather
CIRCUS_ACTS::longest(|#JUGGLING, #TUMBLING|)
-- => "Juggling"
```

None of the three may ask what kind of act it has.
