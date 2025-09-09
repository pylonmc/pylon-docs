# Full code

## Baguette Flamethrower

```java title="MyAddon.java"
NamespacedKey baguetteFlamethrowerKey = new NamespacedKey(this, "baguette_flamethrower");
ItemStack baguetteFlamethrower = ItemStackBuilder.pylonItem(Material.BREAD, baguetteFlamethrowerKey)
        .build();
PylonItem.register(BaguetteFlamethrower.class, baguetteFlamethrower);
BasePages.FOOD.addItem(baguetteFlamethrowerKey);
```

```java title="BaguetteFlamethrower.java"
public class BaguetteFlamethrower extends PylonItem implements PylonItemEntityInteractor {
    private final int burnTimeTicks = getSettings().getOrThrow("burn-time-ticks", Integer.class);

    public BaguetteFlamethrower(@NotNull ItemStack stack) {
        super(stack);
    }

    @Override
    public void onUsedToRightClickEntity(@NotNull PlayerInteractEntityEvent event) {
        event.getRightClicked().setFireTicks(burnTimeTicks);
    }

    @Override
    public @NotNull List<PylonArgument> getPlaceholders() {
        return List.of(
                PylonArgument.of("burn-time", UnitFormat.SECONDS.format(burnTimeTicks / 20.0))
        );
    }
}
```

```yaml title="en.yml"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of baguettes to ignite the entities you look at
    <arrow> <insn>Right click</insn> to ignite the entity you're looking at
    <arrow> <attr>Burn time:</attr> %burn-time%
```

---

## Baguette of Wisdom

```

```
