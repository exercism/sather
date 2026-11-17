# Design

## Goal

Introduce `FILE`: opening a file to read, write or append, writing with
`+`, reading the whole file with `.str`, closing, and checking `.error`. Also
making a folder and deleting a file. The `grep` practice exercise reads
files, and this gives it a prerequisite to name.

## Learning objectives

- Open a file with `FILE::open_for_read`, `FILE::open_for_write` and
  `FILE::open_for_append`, and know which empties the file.
- Write with `+`, remembering that no new line is added.
- Read a whole file with `.str`.
- Close every file that was opened, before returning.
- Check `.error` after opening a file that may not exist, and close only a
  file that opened.
- Make a folder with `FILE::create_directory`, name a file inside it with
  `/`. Deleting a file with `FILE::delete` is taught in the introduction
  but no task needs it.

## Out of scope

- Reading line by line with `get_str` / `get_line`, and the `eof` gotcha.
  about.md covers both.
- `BFILE` (binary files), seeking, `flush`, temporary files.
- Renaming files, removing folders and listing folders. The library has no
  routines for these. They are possible only through shell commands via
  `UNIX::system`, which the track does not teach. about.md says they are
  missing; task 5 copies a file by reading it and writing it again.

## Concepts

- `files`

## Prerequisites

- `string-builders`
- `classes-with-state`: a `FILE` is an object that holds state (open or
  not, where it has read to), and routines are called on it with `.`.

## Notes

The tests write files into the directory the tests run in, which the test
runner makes a writable copy of the solution directory. Each test uses its
own file names, so a test does not depend on files another test left
behind. `day-shift.txt` ships with the exercise as an editor file for task 1.

## Analyzer

None yet. Worth catching: a routine that opens a file and does not close it.
