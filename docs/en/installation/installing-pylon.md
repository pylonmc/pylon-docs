# Installation

!!! danger
    PYLON IS CURRENTLY EXPERIMENTAL. ONLY RUN IT ON A TEST SERVER THAT YOU ARE WILLING TO DELETE. THE NEXT PYLON VERSION WILL PROBABLY NOT BE COMPATIBLE WITH THE PREVIOUS ONE. IF YOU INSTALL PYLON SOMEWHERE YOU SHOULDN'T AND END UP LOSING DATA, WE WILL POINT AND LAUGH AT YOU.

1. Make sure you are running Paper or a Paper fork. Pylon is not compatible with Spigot.
2. Download the latest version of Pylon Core from [here](https://github.com/pylonmc/pylon-core/releases)
3. Download the latest version of Pylon Base from [here](https://github.com/pylonmc/pylon-base)
4. Drop the .jar files in your plugins folder and restart your server. [Do not use /reload](https://madelinemiller.dev/blog/problem-with-reload/). The first start will take longer than usual, but after that, Pylon will load much more quickly.
5. Check out Pylon Core and Pylon Base's plugin folders to see all the config options available.
5. [Install some addons.](list-of-addons.md)
6. That's it!

### Where is Pylon data stored?

You might notice that Pylon does not use a database and does not seem to have any storage files in its plugin folder. This is because Pylon stores everything inside the world file itself in the same way that Minecraft does! You don't need to worry about backing up any data besides your worlds: **Pylon's data will always be consistent with the world's data.** This also means that Pylon is *much* less succeptible to data corruption than other similar plugins.

