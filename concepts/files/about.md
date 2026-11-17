# Files

`FILE` reads and writes text files. It is a thin layer over C's `FILE`, so
it behaves the way C's file routines do.

## Opening

| Call | Opens the file to | If it is not there |
| --- | --- | --- |
| `FILE::open_for_read(name)` | read from the start | `.error` is `true` |
| `FILE::open_for_write(name)` | write, emptying it first | it is created |
| `FILE::open_for_append(name)` | write onto the end | it is created |

Each gives back a new `FILE`. A name with no folder means the folder the
program was started in; `FILE::current_directory` is that folder's full
path.

## Writing

`+` writes a string, a character, or anything else with a `.str`, such as
a number, and gives back the same `FILE`, so writes can be chained:

```sather
   tally ::= FILE::open_for_write("tally.txt");
   tally + "Total: " + 42 + '\n';
   tally.close;
```

Writing is buffered: the text is held in memory and written out in blocks.
`.close` writes whatever is left and lets the file go. `.flush` writes it
out without closing. A file that another part of the program is about to
read should be closed first.

## Reading

`.str` is the whole file as one `STR`. Reading a whole file at once is the
usual way, and the quickest.

`.get_str` reads one line and keeps its `"\n"`. `.eof` becomes `true` only
once a read has tried to go past the end, so a loop that asks `.eof` before
reading gets one empty string after the last line:

```sather
   inp ::= FILE::open_for_read("tally.txt");
   loop
      until!(inp.eof);
      line ::= inp.get_str;     -- "Total: 42\n", then ""
   end;
   inp.close;
```

Reading the whole file with `.str` and then splitting it avoids that.

## Errors

`.error` is `true` when the file could not be opened: reading a file that
is not there, or writing into a folder that does not exist. Reading from,
writing to or closing such a `FILE` stops the program with "Violation of
precondition", so ask `.error` first.

`FILE::delete` and `FILE::create_directory` report nothing. Deleting a file
that is not there, or making a folder that already exists, quietly does
nothing.

## What is not here

The library has no routine to rename or move a file, to remove a folder, or
to list what is in a folder. A file can be moved by reading it, writing the
same text under the new name, and deleting the old one.
