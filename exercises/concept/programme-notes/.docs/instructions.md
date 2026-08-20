# Instructions

Your string group is playing a recital, and somebody has to write the
programme.

All five tasks go in the `PROGRAMME_NOTES` class.

## 1. Name the piece and who wrote it

Put the piece first, then ` by `, then the composer.

```sather
PROGRAMME_NOTES::full_title("Nocturne", "Chopin")
-- => "Nocturne by Chopin"
```

## 2. Measure a line

The printer needs to know how long a line is.

```sather
PROGRAMME_NOTES::title_length("Nocturne")
-- => 8
```

## 3. The first few letters

Given a title and a number, return that many letters from the start.

```sather
PROGRAMME_NOTES::opening_letters("Nocturne", 3)
-- => "Noc"
```

## 4. The last few letters

The same, counting from the end.

```sather
PROGRAMME_NOTES::closing_letters("Nocturne", 4)
-- => "urne"
```

## 5. Shorten a long title

Titles that will not fit are cut to their first six letters, with three
full stops after them.

```sather
PROGRAMME_NOTES::short_title("Nocturne in E flat")
-- => "Noctur..."
```
