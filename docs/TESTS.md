# Tests

## The files

Each exercise comes with three Sather files.
For `hello-world` they are:

| File | Holds |
| --- | --- |
| `hello_world.sa` | your solution, class `HELLO_WORLD` |
| `hello_world_test.sa` | the tests, class `HELLO_WORLD_TEST` |
| `exercism_test.sa` | `EXERCISM_TEST`, which the tests include |

The test class's `main` calls your routines and compares what they return with what they should return.
Every test runs; none are skipped.

## Running the tests

Tests are compiled and run inside the `exercism/sather-test-runner` Docker image, the same one the Exercism website uses.
It includes fixes to GNU Sather 1.2.2 that a copy installed some other way would not have.
See [Installation][installation] for how to set up Docker and download the image.
For now, testing locally is only supported on x86-64 Linux.

From the exercise's directory, run:

```shell
docker run --rm --network none \
    --user "$(id -u):$(id -g)" \
    --mount type=bind,src="$PWD",dst=/work -w /work \
    --entrypoint sh exercism/sather-test-runner -c '
        rm -f hello_world_tests
        sacomp -chk *.sa -main HELLO_WORLD_TEST -o hello_world_tests > /tmp/compile.log 2>&1
        if [ -x hello_world_tests ]; then ./hello_world_tests; else cat /tmp/compile.log; exit 1; fi'
```

This compiles all three files together, with the test class as the program's `main`, and runs the result:

- `--mount ... -w /work` makes the exercise's directory the container's working directory.
- `--user` makes the program it builds, `hello_world_tests`, belong to you rather than to `root`.
- `--entrypoint sh` runs the commands after `-c` in place of the image's own test runner.
- The compiler's output is only shown if the program could not be built.
  A successful build still prints many harmless C compiler warnings, which this hides.

The program prints a summary of the results and exits with a non-zero status if any test failed.
Lines starting `##EX` are for the online test runner, which reads results from them, and can be ignored.

### A shortcut

To avoid typing that for every exercise, add this function to your `~/.bashrc`:

```bash
satest() {
    local test_file exe class
    for test_file in *_test.sa; do
        [ "$test_file" = exercism_test.sa ] || break
    done
    if [ ! -f "$test_file" ] || [ "$test_file" = exercism_test.sa ]; then
        echo "satest: no exercise test file here" >&2
        return 1
    fi
    exe=${test_file%.sa}s
    class=$(basename "$test_file" .sa | tr '[:lower:]' '[:upper:]')
    docker run --rm --network none \
        --user "$(id -u):$(id -g)" \
        --mount type=bind,src="$PWD",dst=/work -w /work \
        --entrypoint sh exercism/sather-test-runner -c "
            rm -f $exe
            sacomp -chk *.sa -main $class -o $exe > /tmp/compile.log 2>&1
            if [ -x $exe ]; then ./$exe; else cat /tmp/compile.log; exit 1; fi"
}
```

Then run `satest` in any exercise's directory.
It finds the test file, and works out the class and program names from it: `two_fer_test.sa` holds `TWO_FER_TEST`.

## Always use `-chk`

`-chk` switches on Sather's runtime checks:

- `pre` and `post` on routines, `assert`, and class invariants
- array bounds
- attribute access through a void reference
- arithmetic overflow

Without it, a contract is read and type-checked but never tested, and a mistake that would have been reported plainly can instead give a wrong answer or crash with no explanation.

The online test runner compiles with `-chk`, so keep it, or a solution that passes on your machine can fail when you submit it.

A broken contract stops the whole program at that point, printing the routine and the source line.
It is not an exception: `protect` does not catch it, and no tests after it run.
When that happens, the contract or the code that called it needs fixing, whichever is wrong.

An exception that nothing catches also stops the program, such as the `raise "unimplemented";` in a routine you have not written yet.

## Submitting

Submit only your solution file:

```shell
exercism submit hello_world.sa
```

The tests and `exercism_test.sa` are supplied by Exercism and are not changed by you.

[installation]: https://exercism.org/docs/tracks/sather/installation
