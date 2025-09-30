# Getting started

Pylon Core is written in [Kotlin](https://kotlinlang.org/), a language similar to Java, but with more modern features and concise syntax. If you know Java, you'll be able to pick up Kotlin very quickly.

Pylon Base is written in Java.

## How to get started

1. Clone the `pylon` repository: `git clone https://github.com/pylonmc/pylon` (or use a GUI like Github Desktop)
2. If you're using IntelliJ, it'll set everything up automatically. If not, run `./gradlew`. This will clone the `pylon-core` and `pylon-base` repositories.
3. If you want to submit your changes to the Pylon project, **delete the `pylon-core` or `pylon-base` directory (depending on which one you want to contribute to), fork the pylon-core or pylon-base repository, and clone your fork into the same directory.** Otherwise, you won't be able to open a pull request with your changes (unless you're a Pylon developer and have access to the Pylon repositories).

See the [Pylon Master Project](./master-project) page for more information about the master repository.

## Submitting your contributions

We generally welcome contributions for both Core and Base, but it's best check with the Pylon team before making any major changes, because we might already have something planned out that won't fit well with your changes. Hop on our Discord server and have a chat with us if you're interested in doing anything major, or have any questions about contributing :)

Once you're done with your changes, open a pull request and give some information about what you did and why you did it.

## Tests

Pylon Core has a set of integration tests. Tests should only be added for critical functionality such as block storage and recipes.

## Custom Dokka

Pylon uses a custom version of Dokka to generate Javadocs. This is because the default Dokka output is very buggy and doesn't look very good. Seggan has submitted pull requests to the Dokka project to fix the issues, but they haven't been merged yet, so in the meantime we use a custom version. If you wish to see the "fixed" doc output, here are the steps:
1. Clone the `pylonmc/dokka` repository: `git clone https://github.com/pylonmc/dokka`
2. Checkout the `pylon` branch: `git checkout pylon`
3. In the root directory, execute `./gradlew publishToMavenLocal -Pversion=2.1.0-pylon-SNAPSHOT`. Note that as Dokka is a very large project, the first build will take a long time. On Seggan's decent-ish laptop, the first run took about 10 minutes. Subsequent builds will be much faster as long s you don't delete the build cache.
4. Now, in the Pylon master project, execute `./gradlew :pylon-core:pylon-core:dokkaGenerate -PusePylonDokka=true`. The generated output will be under `pylon/pylon-core/pylon-core/build/dokka`.

## I'm stuck, what next?

1. If it's Pylon specific, check if it's in the docs. If it's not Pylon specific, google it.
2. Search issues on the relevant repository to see if it's been mentioned
3. Search relevant terms on our Discord server to see if it's been discussed before
4. Ask a question on our Discord server


[comment]: <> (TODO make this easier to comprehend, maybe add screenshots etc, less experienced users will have no idea what the fuck is going on from these instructions)

