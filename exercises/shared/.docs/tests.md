# Tests

The tests are compiled and run inside the `exercism/sather-test-runner` Docker image, the same compiler the Exercism website uses.
For now, testing locally is only supported on x86-64 Linux.
See [Installation][installation] for how to set up Docker.

For an exercise such as `hello-world`, run this from the exercise's directory:

```shell
docker run --rm --network none \
    --user "$(id -u):$(id -g)" \
    --mount type=bind,src="$PWD",dst=/work -w /work \
    --entrypoint sh exercism/sather-test-runner -c '
        rm -f hello_world_tests
        sacomp -chk *.sa -main HELLO_WORLD_TEST -o hello_world_tests > /tmp/compile.log 2>&1
        if [ -x hello_world_tests ]; then ./hello_world_tests; else cat /tmp/compile.log; exit 1; fi'
```

For another exercise, use the name of its test file: `two_fer_test.sa` holds `TWO_FER_TEST`.

Keep `-chk`.
It turns on checking of `pre`, `post`, `assert` and class invariants, as well as array bounds and void access.

[Testing on the Sather track][tests] explains more, and gives a shell function that saves typing the command.

[installation]: https://exercism.org/docs/tracks/sather/installation
[tests]: https://exercism.org/docs/tracks/sather/tests
