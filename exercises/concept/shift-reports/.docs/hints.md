# Hints

## General

- Open a file, use it, then close it, all inside the one routine.
- `FILE::...` routines are called on the class; `+`, `.str`, `.error` and
  `.close` are called on the `FILE` an open gave back.

## 1. Read a report

- Open the file for reading and take its whole contents with `.str`.
- Keep the contents in a variable so the file can be closed before you
  return.

## 2. Check for a report

- Opening a missing file for reading does not stop the program. Look at
  `.error` on what it gives back.
- Only close a file that actually opened.

## 3. Start a report

- Opening for writing empties a file that is already there, which is what
  "starting again replaces it" needs.
- `+` puts in exactly what it is given, so the header needs its `"\n"`.

## 4. Add an entry

- A different open adds to the end instead of emptying the file.

## 5. File a report

- There is no routine that copies a file. Read the report, then write the
  same text under its new name.
- The new name is the folder, a `/`, and the file name.
- Make the folder before writing into it. Making a folder that is already
  there does no harm.
- You have already written a routine that reads a report.
