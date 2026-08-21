# Instructions

You are marking out a walking track through the bush. The distances and the
sightings both come as sequences, so both are iterators.

All four go in the `BUSH_WALK` class. Every one of them is an iterator, so
every name ends in `!`.

## 1. The markers

`markers!` takes a spacing in metres and a count, and gives the distance of
each marker from the start.

```sather
loop
   #OUT + BUSH_WALK::markers!(100, 3) + " ";
end;
-- 100 200 300
```

A count of nought gives nothing at all.

## 2. Until the track ends

`until_end!` takes the sightings along the track and gives them one at a
time, stopping when it meets `"end"`. The `"end"` itself is not given.

```sather
loop
   #OUT + BUSH_WALK::until_end!(|"gum", "wattle", "end", "banksia"|) + " ";
end;
-- gum wattle
```

If there is no `"end"`, it gives everything.

## 3. Only the birds

`birds!` takes the sightings and gives only those that start with a capital
letter, which is how this survey writes birds down.

```sather
loop
   #OUT + BUSH_WALK::birds!(|"gum", "Emu", "wattle", "Galah"|) + " ";
end;
-- Emu Galah
```

## 4. Numbered

`numbered!` takes the sightings and gives each one with its position in
front, counting from one.

```sather
loop
   #OUT + BUSH_WALK::numbered!(|"gum", "Emu"|) + " ";
end;
-- 1. gum 2. Emu
```
