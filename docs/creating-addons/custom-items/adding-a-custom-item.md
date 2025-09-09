# Adding a custom item

## Overview

So far, we've created a 'custom' item in the sense that we've changed the amount of hunger filled up by the baguette from 5 to 6. But what if we want to, for example, be able to right click entities with the baguette to set them on fire? There's no inbuilt way to do this like there was with food. We'll have to write some code to do this for us.

---

## The baguette flamethrower

To illustrate this, let's create a new 'baguette flamethrower' item.

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

In order to do this, we can create a custom `BaguetteFlamethrower` class. All Pylon item classes must extend [PylonItem].

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

We now want to do something whenever the player right clicks on a block while holding the baguette flamethrower. In order to do this, we can implement [PylonItemEntityInteractor] interface. This is a builtin Pylon interface with one method: `onUsedToRightClickEntity`.

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
