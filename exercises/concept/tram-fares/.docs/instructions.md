# Instructions

Melbourne's trams charge by zone, and the city centre is free. You are
writing the fare rules for the ticket machine. All fares are in cents.

All four tasks go in the `TRAM_FARES` class.

## 1. The fare for a zone

Zone 0 is the Free Tram Zone and costs nothing. Zone 1 is 550. Zone 2 is
370. Any other number is not a tram zone at all, and costs nothing.

```sather
TRAM_FARES::zone_fare(1)
-- => 550
TRAM_FARES::zone_fare(7)
-- => 0
```

## 2. What kind of ticket?

Tickets carry a letter. `'f'` is a full fare. Both `'c'` and `'s'` are
concessions — one for children, one for students. `'x'` is a free pass.
Anything else is unknown.

```sather
TRAM_FARES::ticket_kind('s')
-- => "Concession"
TRAM_FARES::ticket_kind('q')
-- => "Unknown"
```

The four answers are `"Full fare"`, `"Concession"`, `"Free pass"` and
`"Unknown"`.

## 3. What kind of day?

`"Sat"` and `"Sun"` are a weekend. `"Mon"` to `"Fri"` are a weekday.
Anything else is unknown.

```sather
TRAM_FARES::day_type("Sun")
-- => "Weekend"
```

The three answers are `"Weekend"`, `"Weekday"` and `"Unknown"`.

## 4. The daily cap

However many trams you take, you never pay more than the cap for that day:
1100 on a weekday and 700 at the weekend. A day nobody recognises has no
cap, which is nought.

```sather
TRAM_FARES::daily_cap("Sat")
-- => 700
```
