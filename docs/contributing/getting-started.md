# Getting started

Pylon Core is written in [Kotlin](https://kotlinlang.org/), a language similar to Java, but with more modern features and concise syntax. If you know Java, you'll be able to pick up Kotlin very quickly.

Pylon Base is written in Java.

## How to get started

1. Clone the `pylon` repository: `git clone https://github.com/pylonmc/pylon` (or use a GUI like Github Desktop)
2. If you're using IntelliJ, it'll set everything up automatically. If not, run `./gradlew`. This will clone the `pylon-core` and `pylon-base` repositories.
3. If you want to submit your changes to the Pylon project, **delete the pylon-core or pylon-base directory (depending on which one you want to contribute to), fork the pylon-core or pylon-base repository, and clone your fork into the same directory.** Otherwise, you won't be able to open a pull request with your changes (unless you're a Pylon developer and have access to the Pylon repositories).
4. To run the tests, open the Gradle menu in IntelliJ, click 'pylon' -> 'pylon' -> 'Tasks' -> 'run paper' -> 'runLiveTests'. If you're not using IntelliJ, run `./gradlew runLiveTests`. This will start a server and run the test addon.
5. To run a server with your local versions of `pylon-core` and `pylon-base`, open the Gradle menu in IntelliJ, click 'pylon' -> 'pylon' -> 'Tasks' -> 'run paper' -> 'runSnapshotServer'. If you're not using IntelliJ, run `./gradlew runSnapshotServer`. This will start a server which you can then join by connecting to `localhost` from Minecraft. The server's files will be located in the `run` directory.

## Submitting your contributions

We generally welcome contributions for both Core and Base, but it's best check with the Pylon team before making any major changes, because we might already have something planned out that won't fit well with your changes. Hop on our Discord server and have a chat with us if you're interested in doing anything major, or have any questions about contributing :)

Once you're done with your changes, open a pull request and give some information about what you did and why you did it.

## Pylon master repository

Pylon has a master repository that contains both `pylon-core` and `pylon-base`. This allows you to run base using your very own home-baked version of core, which allows you to test new features much more easily. This is what the 'How to get started' section used. We recommend you make changes to both base and core using the master repository, and the rest of this guide will assume you're using it.

## Tests

Pylon core has a set of integration tests. Tests should only be added for critical functionality such as block storage and recipes.

## I'm stuck, what next?

1. If it's Pylon specific, check if it's in the docs. If it's not Pylon specific, google it.
2. Search issues on the relevant repository to see if it's been mentioned
3. Search relevant terms on our Discord server to see if it's been discussed before
4. Ask a question on our Discord server


[comment]: <> (TODO make this easier to comprehend, maybe add screenshots etc, less experienced users will have no idea what the fuck is going on from these instructions)

