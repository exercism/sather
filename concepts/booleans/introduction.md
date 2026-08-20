# Booleans

Some questions have only two answers: yes or no. Sather's type for such an
answer is `BOOL`, and the two answers are written `true` and `false`.

```sather
   ready : BOOL is
      return true;
   end;
```

## Comparing

Comparing two numbers gives a `BOOL`.

| Operator | Asks |
| --- | --- |
| `=` | are they the same? |
| `/=` | are they different? |
| `<` | is the left one smaller? |
| `<=` | smaller, or the same? |
| `>` | is the left one bigger? |
| `>=` | bigger, or the same? |

```sather
   old_enough(age : INT) : BOOL is
      return age >= 13;
   end;
```

Note that `=` asks a question. Putting a value *into* something is `:=`,
which you have already seen, and the two are not the same.

## Combining

Three operators build bigger questions out of smaller ones.

`and` is true when **both** sides are true.

```sather
harness_on and rope_checked
```

`or` is true when **either** side is true, or both.

```sather
mat_below or net_below
```

`~` flips an answer over: it turns true into false and false into true.

```sather
~ready       -- true exactly when ready is false
```

`and` and `or` go between two answers; `~` goes in front of one.
