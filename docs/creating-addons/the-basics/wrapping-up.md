# Wrapping up

## The full code

There's been a lot to go through, but when you look at the code we needed, it's actually really not too much:

```java title='YourAddonName.java'
NamespacedKey epicSwordKey = new NamespacedKey(this, "epic_sword");
ItemStack epicSword = ItemStackBuilder.pylonItem(Material.DIAMOND_SWORD, epicSwordKey)
        .set(DataComponentTypes.UNBREAKABLE, Unbreakable.unbreakable())
        .build();
PylonItem.register(PylonItem.class, epicSword);
```

```yml title='en.yml'
addon: "<your addon name here>"

item:
  epic_sword:
    name: "Epic Sword"
    lore: |-
      <arrow> This is an <red>epic</red> sword
      <arrow> Very epic
```

---

## Practice tasks

- Add another item with the same key. What happens?
- Allow your sword to have a stack size greater than 1. **Hint:** Use `DataComponentTypes.MAX_STACK_SIZE`
- Add an epic pickaxe with a different name and lore
- Add a bow that has only 10 durability, and starts with only 5 left. **Hint:** `DataComponentTypes.DAMAGE` and `DataComonentTypes.MAX_DAMAGE` probably don't do what you'd think they do from the name...

---

## What next?

This is only the beginning! We've got a lot more to cover, and we'll be able to go faster now that you know the basics.

In the next section, we'll create a custom item class so we can give our item unique behaviours.

