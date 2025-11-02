# Adding an item

## Overview

The template addon has only one class: `MyAddon` (or whatever you renamed it to). This class extends [JavaPlugin] and implements [PylonAddon]. There are some comments inside the class to explain what each part does - have a read through and try to understand how it works. Our addon doesn't actually do anything yet though - so let's add a new item!

Let's create a baguette, which fills 6 hunger bars, to start with.

To create a simple item, we only need two things: a **key** for the item, and an **item stack**.

---

## Adding the item

### Creating a key

[NamespacedKey]s are how Pylon identifies custom items, blocks, researches, entities, and more.

!!! question "What are NamespaceKeys and why are we using them?"
    A key is just a simple piece of text, like `pylonbase:copper_dust`, which allows Pylon to uniquely identify your item. This is very similar to how vanilla Minecraft items have IDs. Why don't we just use `copper_dust` as the key? Well, what if two addons add an item called `copper_dust`? We won't be able to tell which one is which! To fix this, Pylon uses [NamespacedKey]s, which just means we take a string *and* your addon's name, and put them together - for example, `my_addon:copper_dust`.

To create a new [NamespacedKey] called 'baguette', we can do the following (inside `onEnable`):
=== "Java"
    ```java
    NamespacedKey baguetteKey = new NamespacedKey(this, "baguette");
    ```
=== "Kotlin"
    ```kotlin
    val baguetteKey = NamespacedKey(this, "baguette")
    ```

### Creating the item stack

The second thing we need is an actual item. We'll use [ItemStackBuilder] for this.

[ItemStackBuilder] contains several different methods to help you create [ItemStack]s. For example, you can use `.set(<component>, <value>)` to set some of the item's values, like enchantments, whether the item is unbreakable, and so on.

**Whenever you're creating a Pylon item, make sure you use `ItemStackBuilder.pylonItem(<material>, <key>)`.** There are others ways to create [ItemStack]s, but **do not** use these to create Pylon items. 

??? question "Why use `ItemStackBuilder.pylonItem`, and not any of the other ways to create an [ItemStack]?"
    Under the hood, Pylon stores item keys in [PersistentDataContainer]s, or PDCs. When you call `ItemStackBuilder.pylonItem` and supply a key, that key is written to the item's PDC automatically. If you supply your own item stack, its PDC won't contain the item's key, and Pylon won't be able to differentiate that item with a regular Minecraft item.

    [ItemStackBuilder] also sets the name and lore of the item to the default translation keys (which will be explained later in this tutorial).

To create a baguette, you can do as follows:
=== "Java"
    ```java
    ItemStack baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
            .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
            .build();
    ```
=== "Kotlin"
    ```kotlin
    val baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
        .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
        .build()
    ```

!!! info "Data components"
    Data components are just a way to specify some information about an item - like 'this is a food and it restores 6 hunger', or 'this is a pickaxe and it breaks blocks at XYZ speed'. You can see a full list [here](https://jd.papermc.io/paper/1.21.8/io/papermc/paper/datacomponent/DataComponentTypes.html)

### Registering the item

Next, we need to register our item with Pylon. This means we need to pass two things: the item stack, and the class that should be used to represent the item. We'll cover how to make your own item classes in the next chapter, but for now, you can use the default [PylonItem] class:
=== "Java"
    ```java
    PylonItem.register(PylonItem.class, baguette);
    ```
=== "Kotlin"
    ```kotlin
    PylonItem.register<PylonItem>(baguette)
    ```

### Adding the item to the guide.

Finally, we want to add our item to the Pylon guide. Let's add it to the 'food' section.
=== "Java"
    ```java
    BasePages.FOOD.addItem(baguetteKey);
    ```
=== "Kotlin"
    ```kotlin
    BasePages.FOOD.addItem(baguetteKey)
    ```

---

## Putting it all together

Here's the complete code:
=== "Java"
    ```java title="MyAddon.java" hl_lines="9-14"
        // Called when our plugin is enabled
        @Override
        public void onEnable() {
            instance = this;
    
            // Every Pylon addon must call this BEFORE doing anything Pylon-related
            registerWithPylon();
    
            NamespacedKey baguetteKey = new NamespacedKey(this, "baguette");
            ItemStack baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
                    .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
                    .build();
            PylonItem.register(PylonItem.class, baguette);
            BasePages.FOOD.addItem(baguetteKey);
        }
    ```
=== "Kotlin"
    ```kotlin title="MyAddon.kt" hl_lines="8-13"
        // Called when our plugin is enabled
        override fun onEnable() {
            instance = this
    
            // Every Pylon addon must call this BEFORE doing anything Pylon-related
            registerWithPylon()
    
            val baguetteKey = NamespacedKey(this, "baguette")
            val baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
                .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
                .build()
            PylonItem.register<PylonItem>(baguette)
            BasePages.FOOD.addItem(baguetteKey)
        }
    ```
Now let's test it out!

[JavaPlugin]: https://jd.papermc.io/paper/1.21.8/org/bukkit/plugin/java/JavaPlugin.html
[PylonAddon]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/addon/PylonAddon.html
[NamespacedKey]: https://jd.papermc.io/paper/1.21.8/org/bukkit/NamespacedKey.html
[ItemStackBuilder]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/builder/ItemStackBuilder.html
[ItemStack]: https://jd.papermc.io/paper/1.21.8/org/bukkit/inventory/ItemStack.html
[PylonItem]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/PylonItem.html
[PersistentDataContainer]: https://jd.papermc.io/paper/1.21.8/org/bukkit/persistence/PersistentDataContainer.html
