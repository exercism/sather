# Instructions

Every harness at the circus is rated for a load in kilograms, and nobody
goes up until the numbers have been checked.

The `SAFETY_HARNESS` class needs the following. The stub gives you the class
and its attribute; add the rest. Every routine below carries a contract, and
the hints say which.

## 1. Rig a harness

`create` takes the load the harness is rated for and hands back a harness.
A rating of nought or less is not a harness at all, so that is a `pre`.

```sather
harness ::= #SAFETY_HARNESS(120);
harness.limit
-- => 120
```

## 2. How much is spare?

`spare_capacity` takes the load on the harness and returns how much more it
could take. The load may not be negative, and may not be over the limit —
both `pre`. The answer is never negative, which is a `post`.

```sather
harness.spare_capacity(40)
-- => 80
```

## 3. How full is it?

`percent_used` takes the load and returns it as a percentage of the limit,
rounded down. The load may not be negative, and the answer is never
negative.

```sather
harness.percent_used(60)
-- => 50
```

## 4. Is it safe?

`is_safe` takes the load and answers whether it is within the limit. Any
load at all may be asked about, including a silly one, so there is no `pre`
on the load — but write a `post` saying the answer is true exactly when the
load is within the limit.

```sather
harness.is_safe(200)
-- => false
```
