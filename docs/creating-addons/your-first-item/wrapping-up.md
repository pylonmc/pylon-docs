# Wrapping up

## The full code

There's been a lot to go through, but when you look at the code we needed, it's actually really not too much:

```java title='MyAddon.java'
NamespacedKey baguetteKey = new NamespacedKey(this, "baguette");
ItemStack baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
    .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
    .build();
PylonItem.register(PylonItem.class, baguette);
BasePages.FOOD.addItem(baguetteKey);
```

```yml title='en.yml'
addon: "<your addon name here>"

addon: My Addon
item:
  baguette:
    name: Baguette
    lore: <arrow> <blue>The <white>best <dark_red>food
```

---

## Practice tasks

- Add another item with the same key. What happens?
- Make your baguette's max stack size 32. **Hint:** Use `DataComponentTypes.MAX_STACK_SIZE`
- Add a croissant with a different name and lore
- Add a bow that has only 10 durability, and starts with only 5 left. **Hint:** `DataComponentTypes.DAMAGE` and `DataComonentTypes.MAX_DAMAGE` are somewhat misleadingly named...

---

## What next?

This is only the beginning! We've got a lot more to cover, and we'll be able to go faster now that you know the basics.

In the next section, we'll create a custom item class so we can give our item unique behaviours.

