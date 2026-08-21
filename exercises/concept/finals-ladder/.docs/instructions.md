# Instructions

The netball season is over and the ladder decides who plays finals.

The stub gives you a `TEAM` class. Write `FINALS_LADDER` below it.

## 1. Who is above whom?

`higher` takes two teams and answers whether the first belongs above the
second. More points comes first. Teams level on points are separated by goal
difference, higher first.

```sather
FINALS_LADDER::higher(#TEAM("Vixens", 24, 40), #TEAM("Magpies", 20, 90))
-- => true
```

## 2. The ladder

`ladder` takes the teams in any order and answers them ranked. The array
handed in must be left as it was.

```sather
FINALS_LADDER::ladder(teams)
-- => the same teams, best first
```

## 3. Read the ladder out

`names` takes an array of teams and answers their names joined with `", "`.

```sather
FINALS_LADDER::names(FINALS_LADDER::ladder(teams))
-- => "Vixens, Magpies, Swifts"
```

## 4. The premiers

`premiers` takes the teams in any order and answers the name of the team at
the top. With no teams at all, the answer is `""`.

```sather
FINALS_LADDER::premiers(teams)
-- => "Vixens"
```

## 5. A different order entirely

`shortest_first` takes an array of strings and answers them ordered by
length, shortest first. Strings of the same length go in alphabetical order.

```sather
FINALS_LADDER::shortest_first(|"Magpies", "Vixens", "Swifts"|)
-- => "Swifts", "Vixens", "Magpies"
```

The tie-break is not decoration. The sort is not stable, so without it two
names of the same length could come out either way round.

This is the same sorting routine as task 2, with a different rule handed to
it. That is the point of the exercise.
