# Getting started

## Prerequisites

This guide will assume that you know the basics of Java programming, that you have a Github account, and that you're using [IntelliJ](https://www.jetbrains.com/idea/). This guide also assumes no prior experience with Minecraft plugin development in the first few sections.

### I'm new to programming

If you're new to programming, not to worry, there are plenty of guides online you can follow, and making a Pylon addon is a great way to learn programming. Keep in mind, though, that you will face plenty of challenges along the way! Don't be afraid to look stuff up constantly, and if you're really stuck, join our Discord and somebody will probably be able to help you :)

### I know some programming / have developed a plugin before

You should be able to follow along with this guide fairly easily. Pylon's API is mostly quite simple, while providing a lot of flexibility when you need it.

For more experienced Java programmers, you might also be interested in [Kotlin](https://kotlinlang.org/). This is an alternative to Java. Pylon core is written in Kotlin, since Kotlin is generally nicer to work with (especially in terms of syntax!) and has some cool features that Java is missing. However, this guide will use Java in the interest of being as beginner-friendly as possible.

---

## Setting up your project

### Forking the template

Pylon has an [addon template](https://github.com/pylonmc/pylon-addon-template) you can use, which comes with everything you need to write a Pylon addon. Create a fork of the template. This will create a new repository on Github which will contain your addon code.

TODO the rest of this

---
## Adding your first item

Our addon so far has only one class: `MyAddon` (or whatever you renamed it to). This class extends JavaPlugin and implements PylonAddon. There are some comments inside the class to explain what each part does. Our addon doesn't actually do anything yet though - so let's add a new item!

We'll create an unbreakable diamond sword to start with.

To create a simple item, we only need two things: a **key** for the item, and an **item stack**.

### Creating a key

We need a simple way for Pylon to identify your item - a key. This is very similar to how vanilla Minecraft items have IDs. We could use just a string as the key, but what if two addons add an item called `copper_dust`? We won't be able to tell which one is which! To fix this, Pylon uses `NamespacedKey`s, which just means we take a string *and* your addon's name, and put them together - for example, `my_addon:copper_dust`.

NamespacedKeys are how Pylon identifies custom items, blocks, researches, entities, and more.

To create a new NamespacedKey called 'epic_sword', we can do the following (inside `onEnable`):
```java
NamespacedKey epicSwordKey = new NamespacedKey(this, "epic_sword");
```

### ItemStack

The second thing we need is an actual item.

Whenever you're creating a Pylon item, use `ItemStackBuilder.pylonItem(<material>, <key>)`.

<details>
    <summary>Why use `ItemStackBuilder.pylonItem`?</summary>

    There are others ways to create ItemStacks, but **do not** use these to create Pylon items. Under the hood, Pylon stores item keys in PersistentDataContainers, or PDCs (covered later in the tutorial). When you call ItemStackBuilder.pylonItem and supply a key, that key is written to the item's PersistentDataContainer automatically. If you supply your own item stack, its PDC won't contain the item's key, and Pylon won't be able to differentiate that item with a regular Minecraft item.

    `ItemStackBuilder` also sets the name and lore of the item to the default translation keys (which will be explained later in this tutorial).
</details>

`ItemStackBuilder` contains several different methods to help you create `ItemStack`s. For example, you can use `.set(<component>, <value>)` to set some of the item's values, like enchantments, whether the item is unbreakable, and so on.

To create an unbreakable diamond sword, you can do as follows:
```Java
ItemStack epicSword = ItemStackBuilder.pylonItem(Material.DIAMOND_SWORD, epicSwordKey)
        .set(DataComponentTypes.UNBREAKABLE, Unbreakable.unbreakable())
        .build();
```

### Registering your item

Finally, we need to register our item with Pylon:
```java
PylonItem.register(PylonItem.class, epicSword);
```

### Putting it all together

Here's the complete code:
```java
    // Called when our plugin is enabled
    @Override
    public void onEnable() {
        instance = this;

        // Every Pylon addon must call this BEFORE doing anything Pylon-related
        registerWithPylon();

        NamespacedKey epicSwordKey = new NamespacedKey(this, "epic_sword");
        ItemStack epicSword = ItemStackBuilder.pylonItem(Material.DIAMOND_SWORD, epicSwordKey)
                .set(DataComponentTypes.UNBREAKABLE, Unbreakable.unbreakable())
                .build();
        PylonItem.register(PylonItem.class, epicSword);

    }
```
Now, let's run a server with our plugin.

---

## Running a test server
TODO

## Setting name/lore

Pylon has first-class translation support. Instead of setting an item's name and lore in the code, you'll need to set an item's name and lore in a translation file.

TODO

