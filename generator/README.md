# Test generator

`bin/generate-tests` writes a practice exercise's test file from the exercise's canonical data in [problem-specifications][problem-specifications] and a [Jinja2][jinja] template, `.meta/template.j2`.

For each exercise it:

1. reads `exercises/<slug>/canonical-data.json` from problem-specifications
2. keeps the cases that `.meta/tests.toml` includes (cases marked `include = false`, or missing from `tests.toml`, are left out)
3. appends any track-specific cases from `.meta/additional-test-cases.json`
4. renders `.meta/template.j2`, tidies the whitespace, and writes the test file named in `.meta/config.json`

## Running it

```shell
pip install -r generator/requirements.txt
bin/generate-tests              # every exercise with a template
bin/generate-tests leap sieve   # just these
bin/generate-tests --check      # exit non-zero, with a diff, if a test file is out of date
```

problem-specifications is looked for at `--spec-path`, then `$PROBLEM_SPECIFICATIONS`, then configlet's cache.
Any `bin/configlet sync` run fills and updates the cache, so the usual flow to refresh an exercise is:

```shell
bin/configlet sync --tests --update --exercise leap
bin/generate-tests leap
bin/verify-exercises-in-docker leap
```

## Writing a template

Templates are meant to be read and copied.
A typical one:

```jinja
{% import "macros.j2" as m with context %}
{{ m.begin() }}
{% for case in cases %}

{% set call = "HAMMING::distance(" ~ case.input.strand1 | sa ~ ", " ~ case.input.strand2 | sa ~ ")" %}
{% if case is error %}
{{ m.test_error(case, call) }}
{% else %}
{{ m.test(case, call, case.expected | sa) }}
{% endif %}
{% endfor %}
{{ m.end() }}
```

The macros add no blank lines of their own; the blank line at the top of the loop body separates the tests, and any setup a test needs, such as binding an array argument to a local, can go between it and the test.

Blocks are trimmed (`trim_blocks`, `lstrip_blocks`), trailing whitespace is removed and runs of blank lines are collapsed to one, so spacing in a template needn't be exact.
An undefined variable is an error rather than empty text.

### Variables

| Name             | Value                                                                      |
| ---------------- | -------------------------------------------------------------------------- |
| `cases`          | the included cases, in order: canonical first, then additional             |
| `class_name`     | the solution class, e.g. `HAMMING`                                         |
| `test_class`     | the test class, e.g. `HAMMING_TEST`                                        |
| `slug`           | the exercise slug                                                          |
| `properties`     | the sorted, distinct `property` values of `cases`                          |
| `canonical`      | the whole canonical-data.json object (or `{}` if there is none)            |
| `canonical_url`  | its URL on GitHub                                                          |
| `has_additional` | whether any case came from `additional-test-cases.json`                    |

Each case has the canonical fields (`description`, `property`, `input`, `expected`, `uuid`, `scenarios`, …) and:

| Field              | Value                                                                  |
| ------------------ | ---------------------------------------------------------------------- |
| `full_description` | the descriptions of enclosing groups and the case, joined with `" - "` |
| `groups`           | the descriptions of enclosing groups                                   |
| `index`            | 1-based position in `cases`; unique, for naming locals                 |
| `is_error`         | whether `expected` is `{"error": ...}` (also the test `case is error`) |
| `error`            | the error message, or `None`                                           |
| `additional`       | whether the case came from `additional-test-cases.json`                |

### Filters

| Filter           | Renders                                                                                      |
| ---------------- | -------------------------------------------------------------------------------------------- |
| `sa`             | any JSON value: null as `void`, BOOL, INT, FLTD, STR, or ARRAY of those                      |
| `sa("T")`        | as `sa`, giving the element type of a list (needed if it is empty): `[] \| sa("INT")`        |
| `sa_str`         | a STR literal, escaping `\`, `"`, newline, tab and carriage return; null as `void`           |
| `sa_char`        | a CHAR literal from a one-character string                                                   |
| `sa_int`         | an INT literal; negatives parenthesised; values outside 32 bits are an error                 |
| `sa_inti`        | an INTI expression: `#INTI(153)`, or `#INTI("…")` for integers too large for INT             |
| `sa_flt`         | a FLT literal                                                                                |
| `sa_fltd`        | a FLTD literal                                                                               |
| `sa_bool`        | `true` or `false`                                                                            |
| `sa_array("T")`  | an ARRAY literal with element type `T`, rendering each element as `T`                        |
| `sa_as("T")`     | a value as the named type, e.g. `2 \| sa_as("FLTD")` is `2.0d`                               |
| `sa_type`        | the Sather type `sa` would give a value, e.g. `ARRAY{INT}`                                   |
| `map_str`        | an object as `"key=value"` pairs in key order, joined by commas, to compare with `m.map_str()` |
| `snake`          | `leapYear` → `leap_year`, for routine names                                                  |
| `upper_snake`    | `two-fer` → `TWO_FER`, for class names                                                       |

Besides `error`, there is an `ascii` test: `{% if case.input.value is ascii %}`.
Sather's STR is a string of bytes, so cases with non-ASCII text often need to be left out or handled specially.

Values that don't map onto a literal (objects, say) are best rendered in the template itself, from their fields.

### Macros

`macros.j2` (in this directory) holds the shared macros.
The statement macros emit whole, indented lines, so call them at the start of a line.

| Macro                                       | Emits                                                                                       |
| ------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `m.begin()`                                 | `class …_TEST is`, `include EXERCISM_TEST;`, and the start of `main`                       |
| `{% call m.begin() %}…{% endcall %}`        | the same, with helper routines (the `…`) placed in the class before `main`                  |
| `m.end()`                                   | `finish;` and the end of `main` and the class                                               |
| `m.test(case, actual, expected)`            | `test("…", actual, expected);` for any `$STR` values: INT, BOOL, STR, …                     |
| `m.test_str(case, actual, expected, type)`  | binds `expected` to a local of `type`, then compares `.str` forms, for arrays and the like  |
| `m.test_error(case, call)`                  | a `protect` block expecting `call` to raise the case's error message as a STR               |
| `m.test_error(case, call, returns=false)`   | the same, for a call that returns no value                                                  |
| `m.map_str()`                               | a `map_str(FMAP{STR,INT}) : STR` helper routine, for `m.begin()`'s call block               |

## Track-specific cases

Cases that aren't in the canonical data go in `.meta/additional-test-cases.json`, in the canonical format: a list of cases (or an object with a `cases` list), each with `description`, `property`, `input` and `expected`, and optionally nested in groups.
A `uuid` is not needed.
They are rendered by the same template, after the canonical cases; `case.additional` tells them apart if needed.

[problem-specifications]: https://github.com/exercism/problem-specifications
[jinja]: https://jinja.palletsprojects.com/en/stable/templates/
