# Running your addon

## Starting a test server

The addon template comes with a 'run server' task which you can use to run a test server right in IntelliJ. Just open the Gradle menu and find and double click the `runServer` button. This will start a new server, creating a `run` folder in your project root which will contain the server. You can modify this server however you want - add plugins, change configs, whatever!

![Running the test server](/img/running-test-server.png)

You should see a console pop up with the server output. It'll take a minute or two to download the server executable. It'll fail to start on first run because you'll need to accept the EULA. Go into the `run` folder that was just created and accept the EULA in `eula.txt`, then run the `runServer` task again.

To shut down your server, type `stop` in the console or use `/stop` ingame. **Do not stop the task using the stop button in IntelliJ, because this will not shut down the server.**

Once the server has started, you can connect on `localhost:25565`. Make sure you give yourself admin permissions by typing `op <username>` in the console.

---

## Getting the item

Now, you can give yourself your item. You can do this using `/py give`. For example, `/py give Idra addon-template:epic_sword`. If you've done everything right, you should receive your new sword item. If you try to hit an entity with the sword, you'll notice that it doesn't take damage. The sword is unbreakable!

But wait...

What's going on here?

![Epic sword with missing translation keys](/img/epic-sword-missing-translation-key.png)

Notice that when we created our sword, we didn't give it a name! To do that, we're going to need to use the language system. Don't worry, it's very straightforward - we'll cover it in the next section.

