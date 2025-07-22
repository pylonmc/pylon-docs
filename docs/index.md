## :question: What is Pylon?

Pylon is an upcoming Minecraft Java plugin that will hugely expand vanilla gameplay with new content, including electric machines, huge multiblocks, a fully-fledged fluid system, a complex smelting system, extensive automation options and much, an (actually good) research system, and much more. It is intended to supersede Slimefun.

Pylon uses an addon system, meaning anyone can add content to Pylon by writing an addon for it! It also comes with a number of really useful features, such as:
- First-class translation support, meaning each player can select their own language.
- Extensive configuration options, including per-machine configuration. 
- An intuitive and user-friendly guide to help players figure out the plugin.

## :frame_photo: Pylon in pictures (so far)

![A Pylon fluid setup](/img/fluid-setup.png)
![Hovering over research pack in Pylon guide](/img/hovering-over-research-pack.png)
![Hydraulic fluid setup](/img/hydraulic-fluid-setup.png)
![Copper fluid tank](/img/looking-at-copper-fluid-tank.png)
![Pylon research in the guide](/img/looking-at-research.png)
![Medkit in guide](/img/medkit.png)
![Placing copper pipes](/img/placing-pipes.png)
![Purification tower config](/img/purification-tower-config.png)
![Searching items in the Pylon guide](/img/searching-items.png)
![Using the hydraulic grindstone turner](/img/using-grindstone-turner.png)
![Using the magic altar](/img/using-magic-altar.png)
![Using the smeltery](/img/using-smeltery.png)

## :stopwatch: Performance & stability

We have built Pylon with performance and stability in mind from day 1:

- Pylon makes **extensive** use of caching and will run most performance-intensive systems asynchronously, as well as makeing use of modern concurrency/performance features such as coroutines. 
- In addition, the plugin will have a broad range of config options to help performance - including per-machine tick rates, the ability to limit the number of machines placed by player/chunk/etc, the tick rate of fluid/energy/etc, and more. 
- The way Pylon is designed minimises the chance of data corruption and has a range of error-handling mechanisms if something does go wrong. 
Note: Pylon will likely not be fully compatible with bedrock.

## :calendar: Provisional timeline

**September/October 2025** - Invite-only alpha testing begins.

**Novemeber/December 2025** - Open alpha testing (likely hosted on MetaMechanists - my own server) begins. We will most likely run several seasons of Pylon that each last a few weeks, to iron out bugs, test performance, improve stability and UX, and make sure the plugin is ready to be released.

**Early/mid 2026** - Pylon is officially released

## :keyboard: Developing Pylon addons

We've gone to great lengths to make Pylon easy, intuitive, flexible, and most importantly, fun to develop addons for. A lot of painful lessons learnt from hundreds of hours of Slimefun addon development have guided Pylon's API, and the result is something that's intuitive and easy to work with, while being very flexible. Pylon also fully supports addons written in Kotlin, which is much nicer to write than Java.

Currently, addon development is not supported due to how rapidly Pylon is still changing, and the lack of high-level documentation on how to do it. We plan to soon have a detailed guide on how to create an addon and how to take advantages of all the systems Pylon has to offer, so watch this space!

## :link: Clicky things

Discord invite: [https://discord.gg/4tMAnBAacW](https://discord.gg/4tMAnBAacW)

Github: [https://github.com/pylonmc](https://github.com/pylonmc)

Documentation **(heavy work in progress):** [https://pylonmc.github.io/](https://pylonmc.github.io/)

## :detective: The team

Currently, the core team developing Pylon is:

@seggan :flag_us: - a veteran Slimefun addon developer behind SlimefunWarfare, SFCalc, and the very successful Galactifun addon, with a very impressive contribution record for other addons, the Paper server software, and Slimefun itself. Seggan is responsible for many of the core Pylon systems, including most notably the entire translation system, WAILA, the research system, the internal registry system, and the recipe system (and has done lots more smaller features!).

@ohmvir :flag_ca: - a relatively fresh but enthusiastic face from MetaMechanists who's new to plugin development, but has done a fantastic job getting up to speed and adding lots of base content, like the health talismans and beheading sword, as well as tackling various tasks that need doing here and there.

@overlordidra (me!) :flag_gb: - owner of MetaMechanists (a popular Slimefun server) for over 4 years and the developer behind Quaptics. Many of the core systems - most notably the Pylon guide, the fluid system, hydraulics, the automated test code, and the core systems that keep track of custom blocks/entities/items, are my doing.

We also have help from:

@ihateblueb who has run a Slimefun server (Orchid) and is helping us add more content (the elevator is her doing!).

@.ph.enix who is handling all our CI - he's set up automatic testing on our pull requests, and set up the system to publish new versions of Pylon.

@justahuman_xd who hasn't contributed directly but has a *lot* of Slimefun development experience under his belt and has given a lot of useful input and guidance on the project.

@vaan1310 who has't contributed directly, but has helped with some of the smaller stuff (namely reviewing pull requests).

If you're interested in helping out, drop us a message on our Discord server! You don't have to be an expert to help, a little plugin development experience is enough - there are plenty of tasks to do, ranging from trivial to exceptionally complex, so just let us know if you're interested and we can find something for you to do.

## :question: Got questions?
Drop a message on our Discord server and we'll be happy to answer.
