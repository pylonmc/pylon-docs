# The full code

There's been a lot to go through, but when you look at the code we needed, it's actually really not too much:

=== "Java"
    ```java title='MyAddon.java'
    NamespacedKey baguetteKey = new NamespacedKey(this, "baguette");
    ItemStack baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
        .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
        .build();
    PylonItem.register(PylonItem.class, baguette);
    BasePages.FOOD.addItem(baguetteKey);
    ```
=== "Kotlin"
    ```kotlin title='MyAddon.kt'
    val baguetteKey = NamespacedKey(this, "baguette")
    val baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
        .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
        .build()
    PylonItem.register<PylonItem>(baguette)
    BasePages.FOOD.addItem(baguetteKey)
    ```

```yaml title='en.yml'
addon: "<your addon name here>"

item:
  baguette:
    name: Baguette
    lore: <arrow> <blue>The <white>best <dark_red>food
```
