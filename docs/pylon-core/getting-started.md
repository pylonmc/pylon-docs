# Getting started
`pylon-core` is written in [Kotlin](https://kotlinlang.org/), a JVM language similar to Java, but with more modern features and concise syntax. If you know Java, it's very fast to learn Kotlin.

We use a master pylon repository that contains both `pylon-core` and `pylon-base`. This allows you to run `pylon-base` using your own version of `pylon-core`, which allows you to test new features much more easily.

Pylon core has a set of integration tests. Tests should only be added for critical functionality such as block storage and recipes.

## Local development
- Clone the `pylon` repository: `git clone https://github.com/pylonmc/pylon`
- Run `./gradlew`. This will clone the `pylon-core` and `pylon-base` repositories.
- To run the tests, use `./gradlew runLiveTests`
- To run a server with `pylon-core` and `pylon-base`, use `./gradlew runSnapshotServer`

