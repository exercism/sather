# Hints

## General

- A routine that answers with text is declared `: STR`. One that answers
  with a whole number is declared `: INT`.
- Two arguments of the same type can share a declaration:
  `full_title(piece, composer : STR) : STR`.

## 1. Name the piece and who wrote it

- Three pieces of text joined with `+`: the piece, then `" by "`, then the
  composer.
- The spaces are inside the quotes. `+` adds nothing of its own.

## 2. Measure a line

- `.size`, with no brackets after it.

## 3. The first few letters

- `.head` takes the number in brackets: `title.head(count)`.

## 4. The last few letters

- `.tail` is `.head` counting from the other end.

## 5. Shorten a long title

- Six letters from the front, then `"..."` joined on with `+`.
- The number of letters is always six, so it can be written straight into
  the call rather than passed in.
