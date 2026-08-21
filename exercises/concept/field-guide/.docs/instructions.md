# Instructions

You are keeping a field guide: a map from an animal's name to the habitat it
lives in.

All five tasks go in the `FIELD_GUIDE` class.

## 1. Is it in the guide?

```sather
FIELD_GUIDE::is_listed(guide, "emu")
-- => true
```

## 2. Where does it live?

Return the habitat recorded for an animal. If the guide has never heard of
it, return `"Unknown"`.

```sather
FIELD_GUIDE::habitat_of(guide, "emu")
-- => "grassland"
FIELD_GUIDE::habitat_of(guide, "moa")
-- => "Unknown"
```

## 3. Add an entry

Return the guide with one more animal in it. An animal already listed has
its habitat replaced.

```sather
FIELD_GUIDE::add_entry(guide, "wombat", "forest")
-- => the guide, now with wombat in it
```

Whatever this hands back is the guide to use from then on. Adding to a guide
that is completely empty works and gives a guide with one animal in it.

## 4. How many animals?

```sather
FIELD_GUIDE::entry_count(guide)
-- => 3
```

## 5. Which habitats?

Return the set of habitats the guide mentions. Several animals may share a
habitat, and it should appear once.

```sather
FIELD_GUIDE::all_habitats(guide)
-- => a set holding "grassland" and "forest"
```
