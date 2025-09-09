# Making items configurable

## Overview

Let's add a config so server owners can change how long the baguette flamethrower sets entities on fire for.

---

## Creating the config file

If you look inside your server's Pylon settings directory (`run/plugins/PylonCore/settings/pylonbase`) you'll see that every item and every block has its own config file.

For example, `bandage.yml` contains:

```yaml title="bandage.yml"
consume-seconds: 1.25
heal-amount: 4.0
```

We want to add our own config file which lets you choose how long the baguette flamethrower sets entities on fire for.

Create a new file `resources/settings/baguette_flamethrower.yml` and add the following:

```yaml title="baguette_flamethrower.yml"
burn-time-ticks: 40
```

!!! success "Best practice"
    When your config option is a quantity, include the unit in the name. If we just called it `burn-time`, users might not know that it's in ticks, and assume it's in seconds or something else.

Pylon will automatically copy all of your settings files into `run/plugins/PylonCore/settings/<your-addon-name>` when the settings file is first used.

---

## Using the config file

To read the `burn-time-ticks` value from the config file, we can use `getSettings().getOrThrow(...)`:

```java title="BaguetteFlamethrower.java" hl_lines="2"
public class BaguetteFlamethrower extends PylonItem implements PylonItemEntityInteractor {
    private final int burnTimeTicks = getSettings().getOrThrow("burn-time-ticks", Integer.class);

    public BaguetteFlamethrower(@NotNull ItemStack stack) {
        super(stack);
    }

    @Override
    public void onUsedToRightClickEntity(@NotNull PlayerInteractEntityEvent event) {
        event.getRightClicked().setFireTicks(40);
    }
}
```

!!! question "How does Pylon know which config file to use?"
    Config files are actually per **key**, not per item. When calling `getSettings()`, all this does is take the item's key and find the settings file for it! It's just a shorthand for `Settings.get(getKey())`. If you used `Settings.get(new NamespacedKey(MyAddon.getInstance(), "buffoon"))` then the `buffoon.yml` settings file would be read instead.

!!! question "Why are we using `getOrThrow` instead of `get`?"
    Settings also have a `get` method. This method just returns null if the key was not found, so it should only be used where you don't necessarily *need* the key. If you use `getOrThrow`, a nice exception will be thrown with some information on what key is missing and where.

And now we can use that value when setting entities on fire!

```java title="BaguetteFlamethrower.java" hl_lines="10"
public class BaguetteFlamethrower extends PylonItem implements PylonItemEntityInteractor {
    private final int burnTimeTicks = getSettings().getOrThrow("burn-time-ticks", Integer.class);

    public BaguetteFlamethrower(@NotNull ItemStack stack) {
        super(stack);
    }

    @Override
    public void onUsedToRightClickEntity(@NotNull PlayerInteractEntityEvent event) {
        event.getRightClicked().setFireTicks(burnTimeTicks);
    }
}
```

Try changing the config value, and the burn time should change with it.

!!! danger
    The run server task deletes everything inside the `plugins` folder whenever it's run, meaning any changes you make to your new config there will be overwritten. Instead, just try changing the default value - or run the server manually so the `plugins` folder isn't deleted when the server restarts.
