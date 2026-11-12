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
   overdue(days_out : INT) : BOOL is
      return days_out > 21;
   end;
```

`=` compares; it doesn't change anything.

## Combining

Three operators build bigger questions out of smaller ones.

`and` is true when **both** sides are true.

```sather
has_card and paid_up
```

`or` is true when **either** side is true, or both.

```sather
on_shelf or on_order
```

`~` flips an answer over: it turns true into false and false into true.

```sather
~ready       -- true exactly when ready is false
```

`and` and `or` go between two answers; `~` goes in front of one.
