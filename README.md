# Exercism Sather Track

[![Configlet](https://github.com/exercism/sather/actions/workflows/configlet.yml/badge.svg)](https://github.com/exercism/sather/actions/workflows/configlet.yml) [![Test](https://github.com/exercism/sather/actions/workflows/test.yml/badge.svg)](https://github.com/exercism/sather/actions/workflows/test.yml)

Exercism exercises in Sather.

## Testing

To check that every exercise's example or exemplar solution passes its tests, run:

```shell
bin/verify-exercises-in-docker
```

This compiles and runs each exercise in the [`exercism/sather-test-runner`][test-runner] Docker image, the same image the Exercism website uses, so you only need Docker installed.
CI runs the same script.
To test one exercise, run `bin/verify-exercises-in-docker <exercise-slug>`.
To test against a locally built test runner image, add `-i <image>`.

`bin/verify-exercises` takes the same arguments.
Instead of running the test runner, it compiles each exercise with `sacomp -chk` in the same image and runs the tests, as [students are told to][tests].
It prints the compiler's errors and each test's result directly, so it's handier when a test fails.

### Linting

[`configlet`](https://exercism.org/docs/building/configlet) is an Exercism-wide tool for working with tracks. You can download it by running:

```shell
$ ./bin/fetch-configlet
```

Run its [`lint` command](https://exercism.org/docs/building/configlet/lint) to verify if exercises have the required files and if config files are correct:

```shell
$ ./bin/configlet lint

The lint command is under development.
Please re-run this command regularly to see if your track passes the latest linting rules.

Basic linting finished successfully:
- config.json exists and is valid JSON
- config.json has these valid fields:
    language, slug, active, blurb, version, status, online_editor, key_features, tags
- Every concept has the required .md files
- Every concept has a valid links.json file
- Every concept has a valid .meta/config.json file
- Every concept exercise has the required .md files
- Every concept exercise has a valid .meta/config.json file
- Every practice exercise has the required .md files
- Every practice exercise has a valid .meta/config.json file
- Required track docs are present
- Required shared exercise docs are present
```

## Adding exercises

New (practice) exercises can be added via:

```shell
bin/add-practice-exercise <exercise-slug>
```

Optionally, you can also specify the exercise's difficulty (via `-d`) and/or author's GitHub username (via `-a`):

```shell
bin/add-practice-exercise -a foobar -d 3 <exercise-slug>
```

The script copies in the test harness and, when the exercise has canonical data, a starting `.meta/template.j2`.

## Generating tests

Practice exercise test files are generated from [problem-specifications][problem-specifications] canonical data by `bin/generate-tests`, using each exercise's `.meta/template.j2`:

```shell
pip install -r generator/requirements.txt
bin/generate-tests              # every exercise with a template
bin/generate-tests leap         # one exercise
bin/generate-tests --check      # report test files that are out of date
```

See [generator/README.md](generator/README.md) for how templates are written.

## Track checks

These scripts enforce the track's own rules:

| Script | Checks |
| --- | --- |
| `bin/check-syllabus` | each concept exercise teaches one concept, introductions match, and exercises follow their prerequisites (run in CI) |
| `bin/check-answer-leaks` | concept docs and hints don't give away an exemplar's code |
| `bin/check-accretive` | a student who finishes the first *K* tasks of a concept exercise sees those tasks' tests pass (see [accretive-audit.md](accretive-audit.md)) |
| `bin/reorder-exercises` | sorts practice exercises in `config.json` by difficulty, then name (order checked in CI) |

[test-runner]: https://github.com/exercism/sather-test-runner
[tests]: docs/TESTS.md
[problem-specifications]: https://github.com/exercism/problem-specifications
