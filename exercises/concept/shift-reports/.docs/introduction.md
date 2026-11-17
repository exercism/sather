# Files

A `FILE` is a file on disk that a program has opened. Opening one gives a
`FILE` object, and the program reads or writes through it.

## Writing a file

`FILE::open_for_write` opens a file for writing. If the file is not there
it is created; if it is, everything in it is thrown away first.

```sather
   log ::= FILE::open_for_write("rainfall.txt");
   log + "Rain gauge readings\n";
   log + "Monday " + 12 + "mm\n";
   log.close;
```

`+` writes onto the end of the file, the same way `+` adds onto `#OUT`.
Nothing puts a new line in for you, so `"\n"` ends each line.

## Closing

`.close` finishes with the file. Writing is saved up and done in batches,
and closing is what makes sure the last batch reaches the disk. Close a
file before anything else reads it, or the reader may find it shorter than
it should be.

## Adding to a file

`FILE::open_for_append` opens a file and writes onto the end of what is
already there. If the file is not there yet, it is created.

```sather
   log ::= FILE::open_for_append("rainfall.txt");
   log + "Tuesday " + 3 + "mm\n";
   log.close;
```

## Reading a file

`FILE::open_for_read` opens a file for reading, and `.str` gives everything
in it as one `STR`, new lines included.

```sather
   log ::= FILE::open_for_read("rainfall.txt");
   readings ::= log.str;
   log.close;
   -- readings is "Rain gauge readings\nMonday 12mm\nTuesday 3mm\n"
```

## A file that is not there

Opening a file that does not exist for reading does not stop the program.
It gives back a `FILE` that is not attached to anything, and `.error` on it
is `true`.

```sather
   gauge ::= FILE::open_for_read("snowfall.txt");
   if gauge.error then
      #OUT + "No snowfall records\n";
   else
      #OUT + gauge.str;
      gauge.close;
   end;
```

Ask `.error` before anything else. Reading from that `FILE`, or closing
it, stops the program.

## Folders

A file in a folder is named with a `/` between the folder and the file:
`"2024/rainfall.txt"` is `rainfall.txt` inside the folder `2024`.

`FILE::create_directory` makes a folder. Making one that is already there
does no harm.

```sather
   FILE::create_directory("2024");
   log ::= FILE::open_for_write("2024/rainfall.txt");
```

## Deleting a file

`FILE::delete` removes a file.

```sather
   FILE::delete("rainfall-draft.txt");
```

`FILE::open_for_write`, `FILE::open_for_append`, `FILE::open_for_read`,
`FILE::create_directory` and `FILE::delete` are called on the class itself,
with `::`. `+`, `.str`, `.error` and `.close` are called on the `FILE` that
an open gave back.
