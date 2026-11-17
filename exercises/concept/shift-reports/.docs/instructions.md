# Instructions

The Port Kembla steelworks runs around the clock, and every shift keeps a
report: a text file that starts with a header line and gets one line added
for each thing that happens. You are writing the routines that look after
those reports.

All five tasks go in the `SHIFT_REPORTS` class. Each report is named by its
file name, such as `"day-shift.txt"`.

## 1. Read a report

Return everything in a report, exactly as it is in the file.

```sather
SHIFT_REPORTS::read_report("day-shift.txt")
-- => "Shift: Day\nBlast furnace tapped at 7:40\nCoke ovens running normally\nSlab caster stopped for a roll change\n"
```

The day shift's report comes with the exercise, so you can open
`day-shift.txt` to see it.

## 2. Check for a report

Return whether a report exists.

```sather
SHIFT_REPORTS::has_report("day-shift.txt")
-- => true
SHIFT_REPORTS::has_report("maintenance.txt")
-- => false
```

## 3. Start a report

Start a new report: a file holding only its header line, which is
`Shift: ` followed by the shift's name, and ends with a new line.

```sather
SHIFT_REPORTS::start_report("night-shift.txt", "Night");
SHIFT_REPORTS::read_report("night-shift.txt")
-- => "Shift: Night\n"
```

If the report was already there, starting it again replaces it.

## 4. Add an entry

Add a line to the end of a report. The entry is given without a new line,
and the report should end with one.

```sather
SHIFT_REPORTS::add_entry("night-shift.txt", "Mill started at 22:05");
SHIFT_REPORTS::read_report("night-shift.txt")
-- => "Shift: Night\nMill started at 22:05\n"
```

## 5. File a report

At the end of the day, a copy of each report is filed in a folder named
after the day. Copy the report into the folder, keeping its file name. The
original stays where it was. The folder may not exist yet.

```sather
SHIFT_REPORTS::file_report("night-shift.txt", "monday");
SHIFT_REPORTS::read_report("monday/night-shift.txt")
-- => "Shift: Night\nMill started at 22:05\n"
SHIFT_REPORTS::has_report("night-shift.txt")
-- => true
```
