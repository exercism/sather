# Installation

The Sather track compiles your code with the same GNU Sather compiler the Exercism website uses.
That compiler comes in a Docker image, `exercism/sather-test-runner`, so you don't need to build or install Sather yourself.

For now, testing locally is only supported on x86-64 Linux.
On all platforms, you can solve the exercises in the online editor on the Exercism website.

## The Exercism CLI

To download exercises and submit your solutions, install the [Exercism CLI][cli].

## Docker

Install Docker Engine by following the [instructions for your Linux distribution][docker-install].

Then follow the [post-installation steps][docker-postinstall], so that you can run `docker` without `sudo`.

Download the image:

```shell
docker pull exercism/sather-test-runner
```

Run the same command again from time to time to pick up updates.

Once both are installed, see [Testing on the Sather track][tests] for how to run the tests.

[docker-install]: https://docs.docker.com/engine/install/
[docker-postinstall]: https://docs.docker.com/engine/install/linux-postinstall/
[cli]: https://exercism.org/docs/using/solving-exercises/working-locally
[tests]: https://exercism.org/docs/tracks/sather/tests
