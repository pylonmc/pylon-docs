# Making items configurable

## Overview

Items can have configs associated with them. If you look inside your server's Pylon settings directory (`run/plugins/PylonCore/settings/pylonbase`) you'll see that every item and every block has its own config file.

For example, `bandage.yml` contains:

```yaml title="bandage.yml"
consume-seconds: 1.25
heal-amount: 4.0
```

---

## Creating the config file

Suppose we want to add our own config file which lets you choose how long the baguette flamethrower sets entities on fire for.

Create a new file `resources/settings/baguette_flamethrower.yml` and add the following:

```yaml title="baguette_flamethrower.yml"
burn-time-ticks: 40
```

!!! success "Best practice"
    When your config option is a quantity, include the unit in the name. If we just called it `burn-time`, users might not know that it's in ticks, and assume it's in seconds or something else.

Pylon will automatically copy all of your settings files into `run/plugins/PylonCore/settings/<your-addon-name>` when the settings file is first used, so that server owners can configure items.

---

## Reading the config file

To read the `burn-time-ticks` value from the config file, we can use `getSettings().getOrThrow(...)`. `getSettings()` will just return the config with the same name as the item key - in this case `flamethrower_baguette`:

=== "Java"
    ```java title="BaguetteFlamethrower.java" hl_lines="2"
    public class BaguetteFlamethrower extends PylonItem implements PylonItemEntityInteractor {
        private final int burnTimeTicks = getSettings().getOrThrow("burn-time-ticks", ConfigAdapter.INT);
    
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
    ```kotlin title="BaguetteFlamethrower.kt" hl_lines="2"
    class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
        private val burnTimeTicks = settings.getOrThrow("burn-time-ticks", ConfigAdapter.INT)
    
        override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
            event.rightClicked.fireTicks = 40
        }
    }
    ```
!!! question "How does Pylon know which config file to use?"
    Config files are actually per **key**, not per item. When accessing `settings`, all this does is take the item's key and find the settings file for it! It's just a shorthand for `Settings.get(key)`. If you used `Settings.get(NamespacedKey(MyAddon.instance, "buffoon"))` then the `buffoon.yml` settings file would be read instead.

Settings also have a `get` method. This method just returns null if the key was not found. If you use `getOrThrow`, a nice exception will be thrown with some information on what key is missing and where.

When calling `get` or `getOrThrow`, we have to supply a ConfigAdapter. This is a class that contains instructions on how to exactly read a value from a config file.

!!! You can find a list of config adapters [here](TODO)

## Using the values we read from the config file

And now we can use that value when setting entities on fire!

=== "Java"
    ```java title="BaguetteFlamethrower.java" hl_lines="10"
    public class BaguetteFlamethrower extends PylonItem implements PylonItemEntityInteractor {
        private final int burnTimeTicks = getSettings().getOrThrow("burn-time-ticks", ConfigAdapter.INT);
    
        public BaguetteFlamethrower(@NotNull ItemStack stack) {
            super(stack);
        }
    
        @Override
        public void onUsedToRightClickEntity(@NotNull PlayerInteractEntityEvent event) {
            event.getRightClicked().setFireTicks(burnTimeTicks);
        }
    }
    ```
=== "Kotlin"
    ```kotlin title="BaguetteFlamethrower.kt" hl_lines="5"
    class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
        private val burnTimeTicks = settings.getOrThrow("burn-time-ticks", ConfigAdapter.INT)
    
        override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
            event.rightClicked.fireTicks = burnTimeTicks
        }
    }
    ```

If you change the config value, the burn time should change with it.

!!! danger
    When testing configs, keep in mind that the run server task deletes everything inside the `plugins` folder whenever it's run, meaning any changes you make to your new config there will be overwritten. Instead, just try changing the default value - or run the server manually so the `plugins` folder isn't deleted when the server restarts.
