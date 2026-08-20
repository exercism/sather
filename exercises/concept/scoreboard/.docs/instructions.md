# Instructions

You are running the scoreboard at a netball match. Unlike everything so far,
a scoreboard has to remember what has happened.

The `SCOREBOARD` class needs the following. The stub gives you the class and
its two attribute declarations; add the rest.

## 1. Set up the board

`create` takes the home team's name and the away team's name, and hands back
a scoreboard with both scores at nought.

```sather
board ::= #SCOREBOARD("Vixens", "Magpies");
board.home_score
-- => 0
```

## 2. Score a goal

`home_goal` adds one to the home score, and `away_goal` adds one to the away
score. Neither answers anything.

```sather
board.home_goal;
board.home_score
-- => 1
```

## 3. Read the board

`summary` returns the board as it would be written up: the home team, its
score, a dash, the away score, then the away team.

```sather
board.summary
-- => "Vixens 1 - 0 Magpies"
```

The spaces are exactly as shown, and the dash is a single `-`.

## 4. Who is winning?

`leader` returns the name of the team ahead, or `"Draw"` when the scores are
level.

```sather
board.leader
-- => "Vixens"
```

## 5. How far ahead?

`margin` returns how many goals separate the teams. It is never negative,
whoever is ahead.

```sather
board.margin
-- => 1
```
