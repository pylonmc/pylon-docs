# Getting started

## Foreword

So, you want to write a Pylon addon? Good for you! We've written this comprehensive guide to try and make it as easy as possible. Don't be too intimidated by the wall of text - we'll explain all you need to know as we go along, and you can go as slow as you need to! That said, some basic technical and programming knowledge is required - if you've never used an IDE or a compiler, or never a for loop, you might have a hard time following.

Some housekeeping before we start...

### Prerequisites

We'll assume that 

- you know the basics of Java programming
- you have a Github account
- you have some way to use git from your computer - we recommend [Github Desktop](https://github.com/apps/desktop).
- you've installed and set up [IntelliJ](https://www.jetbrains.com/idea/) and have some idea of how to use it.

No prior plugin development knowledge is required, though it would certainly be useful!

### A note on Kotlin

Though you can write addons in Java just fine, more experienced Java programmers might be interested in [Kotlin](https://kotlinlang.org/). This is an alternative to Java which is much nicer to work with (especially in terms of syntax!) and has some cool features that Java is missing. Pylon Core is written in Kotlin.

Now let's get into it!

---

## Setting up

### Forking the template

Pylon has an [addon template](https://github.com/pylonmc/pylon-addon-template) you can use, which comes with everything you need to write a Pylon addon. [Create a fork of the template](https://www.geeksforgeeks.org/git/how-to-fork-a-github-repository/). Then, [clone your fork](https://www.geeksforgeeks.org/git/how-to-git-clone-a-remote-repository/).

Next, open your fork in Intellij. 

It might take a few minutes for Intellij to import the project.

![Intellij importing the addon template](/img/importing-addon-template.png)

### What's in the template?

The template is as minimal as possible and contains no fluff. It's built with [gradle](https://gradle.org/). There are two files in the root of the directory - `gradlew` and `gradlew.bat` which are wrappers around gradle. If you're using Intellij, you won't need to worry about them. There's also `build.gradle.kts`, which you'll only need to worry about if you want to add dependencies or want to change the way the project is built.

What you *do* need to worry about is `build.gradle.kts` and `gradle.properties` These two files contain the top-level information about your project - name, version, Pylon core version, main class, and group. Make sure you change these accordingly. If you're confused about the 'main class' and 'group', [this might help.](https://www.baeldung.com/java-packages)

Finally, we've got `AddonTemplate.java`. This is the important bit! Open it up, and we'll continue from there in the next tutorial.

