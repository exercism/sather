# Instructions

You are calling the cues for your school's production. The stage manager
wants the standard lines written down so that anyone can run the desk.

You have four tasks, all in the `STAGE_DIRECTIONS` class.

## 1. Announce the start

Return the line that opens the show.

```sather
STAGE_DIRECTIONS::opening_line
-- => "The curtain rises."
```

## 2. Announce the interval

Return the line called at half time.

```sather
STAGE_DIRECTIONS::interval_line
-- => "Interval. Fifteen minutes."
```

## 3. Announce the end

Return the line that closes the show.

```sather
STAGE_DIRECTIONS::closing_line
-- => "The curtain falls."
```

## 4. Call the final cue

The final cue is the same line as the one that closes the show. Rather than
writing the text out a second time, call the routine you already wrote.

```sather
STAGE_DIRECTIONS::final_cue
-- => "The curtain falls."
```
