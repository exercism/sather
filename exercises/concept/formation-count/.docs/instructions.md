# Instructions

The dance troupe is working out its end-of-year show: how many ways the
dancers can be arranged, and how the running time divides between the acts.

All five tasks go in the `FORMATION_COUNT` class.

## 1. How many line-ups?

With `n` dancers there are `n` factorial ways to line them up: `n` choices
for the front, then `n-1` for the next, and so on. Return that as an `INTI`.
Nought dancers have exactly one line-up — the empty one.

```sather
FORMATION_COUNT::line_ups(5)
-- => 120
FORMATION_COUNT::line_ups(20)
-- => 2432902008176640000
```

## 2. Write it out

The same number as a string, every digit of it.

```sather
FORMATION_COUNT::line_ups_text(25)
-- => "15511210043330985984000000"
```

An `INT` cannot hold that number, which is the point of the task.

## 3. One act's share

A show of `acts` equal acts gives each act `1/acts` of the running time.
Return that as a `RAT`.

```sather
FORMATION_COUNT::share(3)
-- => 1/3
```

## 4. Two acts together

Add two shares and return the total, exactly.

```sather
FORMATION_COUNT::combined(FORMATION_COUNT::share(2), FORMATION_COUNT::share(3))
-- => 5/6
```

## 5. Does it fill the show?

Answer whether a share is exactly the whole show — that is, exactly one.

```sather
FORMATION_COUNT::covers_whole_show(#RAT(3, 3))
-- => true
FORMATION_COUNT::covers_whole_show(#RAT(2, 3))
-- => false
```
