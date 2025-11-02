# Adding a custom item

## Overview

This section describes how to attach custom behaviour to an item. We'll demonstrate this by creating a baguette flamethrower which sets entities on fire when they are right clicked.

---

## The baguette flamethrower

### Creating a 'normal item'

Let's start by making a 'normal' item, like we did in the previous chapter.

=== "Java"
    ```java title="MyAddon.java"
    NamespacedKey baguetteFlamethrowerKey = new NamespacedKey(this, "baguette_flamethrower");
    ItemStack baguetteFlamethrower = ItemStackBuilder.pylonItem(Material.BREAD, baguetteFlamethrowerKey)
            .build();
    PylonItem.register(PylonItem.class, baguetteFlamethrower);
    BasePages.FOOD.addItem(baguetteFlamethrowerKey);
    ```
=== "Kotlin"
    ```kotlin title="MyAddon.kt"
    val baguetteFlamethrowerKey = NamespacedKey(this, "baguette_flamethrower")
    val baguetteFlamethrower = ItemStackBuilder.pylonItem(Material.BREAD, baguetteFlamethrowerKey)
        .build()
    PylonItem.register<PylonItem>(baguetteFlamethrower)
    BasePages.FOOD.addItem(baguetteFlamethrowerKey)
    ```

```yaml title="en.yml"
item:
  baguette_flamethrower:
    name: "Baguette Flamethrower"
    lore: |-
      <arrow> Use the power of baguettes to ignite the blocks you look at
```

### Creating a custom item class

Next, we'll add the code to set entities on fire.

In order to do this, we must create a custom `BaguetteFlamethrower` class. All Pylon item classes must extend [PylonItem].

=== "Java"
    Create a new file `BaguetteFlamethrower.java` and add the following:
    
    ```java title="BaguetteFlamethrower.java"
    public class BaguetteFlamethrower extends PylonItem {
        public BaguetteFlamethrower(@NotNull ItemStack stack) {
            super(stack);
        }
    }
    ```
=== "Kotlin"
    Create a new file `BaguetteFlamethrower.kt` and add the following:
    
    ```kotlin title="BaguetteFlamethrower.kt"
    class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack)
    ```

We now want to run some code when the player right clicks on an entity while holding the baguette flamethrower. In order to do this, we need to implement a Pylon item interface. 

Pylon item interfaces are just interfaces that add different behaviours to items, like running some code when the item is used.

Here, we need to implement the [PylonItemEntityInteractor] interface. This interface has one method: `onUsedToRightClickEntity`.

!!! note You can find a full list of item interfaces [here](https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/base/package-summary.html).

=== "Java"
    ```java title="BaguetteFlamethrower" hl_lines="6-9"
    public class BaguetteFlamethrower extends PylonItem implements PylonItemEntityInteractor {
        public BaguetteFlamethrower(@NotNull ItemStack stack) {
            super(stack);
        }
    
        @Override
        public void onUsedToRightClickEntity(@NotNull PlayerInteractEntityEvent event) {
            event.getRightClicked().setFireTicks(40);
        }
    }
    ```
=== "Kotlin"
    ```kotlin title="BaguetteFlamethrower" hl_lines="2-4"
    class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
        override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
            event.rightClicked.fireTicks = 40
        }
    }
    ```

### Using the custom item class

In order to use this class, we now need to specify that the baguette flamethrower should use it instead of the default `PylonItem` class.

Change your `PylonItem.register(...)` line to the following:

=== "Java"
    ```java
    PylonItem.register(BaguetteFlamethrower.class, baguette);
    ```
=== "Kotlin"
    ```kotlin
    PylonItem.register<BaguetteFlamethrower>(baguette)
    ```

And that's it! Now, try running the server. When you right click an entity with the baguette flamethrower, you should set it on fire for 40 ticks!

[PylonItem]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/PylonItem.html
[PylonItemEntityInteractor]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/base/PylonItemEntityInteractor.html
