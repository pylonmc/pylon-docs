# Full code

## Baguette Flamethrower

=== "Java"
    ```java title="MyAddon.java"
    NamespacedKey baguetteFlamethrowerKey = new NamespacedKey(this, "baguette_flamethrower");
    ItemStack baguetteFlamethrower = ItemStackBuilder.pylonItem(Material.BREAD, baguetteFlamethrowerKey)
            .build();
    PylonItem.register(BaguetteFlamethrower.class, baguetteFlamethrower);
    BasePages.FOOD.addItem(baguetteFlamethrowerKey);
    ```
=== "Kotlin"
    ```kotlin title="MyAddon.kt"
    val baguetteFlamethrowerKey = NamespacedKey(this, "baguette_flamethrower")
    val baguetteFlamethrower = ItemStackBuilder.pylonItem(Material.BREAD, baguetteFlamethrowerKey)
        .build()
    PylonItem.register<BaguetteFlamethrower>(baguetteFlamethrower)
    BasePages.FOOD.addItem(baguetteFlamethrowerKey)
    ```

[](tab break)

=== "Java"
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
=== "Kotlin"
    ```kotlin title="BaguetteFlamethrower.kt"
    class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
        private val burnTimeTicks = settings.getOrThrow("burn-time-ticks", Int::class.java)
    
        override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
            event.rightClicked.fireTicks = burnTimeTicks
        }
    
        override fun getPlaceholders() =
            listOf(PylonArgument.of("burn-time", UnitFormat.SECONDS.format(burnTimeTicks / 20.0)))
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

=== "Java"
    ```java title="MyAddon.java"
    NamespacedKey baguetteOfWisdomKey = new NamespacedKey(this, "baguette_of_wisdom");
    ItemStack baguetteOfWisdom = ItemStackBuilder.pylonItem(Material.BREAD, baguetteOfWisdomKey)
            .editPdc(pdc -> pdc.set(
                    BaguetteOfWisdom.STORED_XP_KEY,
                    PylonSerializers.INTEGER,
                    0
            ))
            .build();
    PylonItem.register(BaguetteOfWisdom.class, baguetteOfWisdom);
    BasePages.FOOD.addItem(baguetteOfWisdomKey);
    ```
=== "Kotlin"
    ```kotlin title="MyAddon.kt"
    val baguetteOfWisdomKey = NamespacedKey(this, "baguette_of_wisdom")
    val baguetteOfWisdom = ItemStackBuilder.pylonItem(Material.BREAD, baguetteOfWisdomKey)
        .editPdc { pdc ->
            pdc.set(
                BaguetteOfWisdom.STORED_XP_KEY,
                PylonSerializers.INTEGER,
                0
            )
        }
        .build()
    PylonItem.register<BaguetteOfWisdom>(baguetteOfWisdom)
    BasePages.FOOD.addItem(baguetteOfWisdomKey)
    ```

[](tab break)

=== "Java"
    ```java title="BaguetteOfWisdom.java"
    public class BaguetteOfWisdom extends PylonItem implements PylonInteractor {
        public static final NamespacedKey STORED_XP_KEY = new NamespacedKey(MyAddon.getInstance(), "stored_xp");
    
        private final int xpCapacity = getSettings().getOrThrow("xp-capacity", Integer.class);
    
        public BaguetteOfWisdom(@NotNull ItemStack stack) {
            super(stack);
        }
    
        @Override
        public @NotNull List<PylonArgument> getPlaceholders() {
            return List.of(
                    PylonArgument.of("xp_capacity", UnitFormat.EXPERIENCE.format(xpCapacity)),
                    PylonArgument.of("stored_xp", UnitFormat.EXPERIENCE.format(getStoredXp()))
            );
        }
    
        @Override
        public void onUsedToRightClick(@NotNull PlayerInteractEvent event) {
            if (event.getPlayer().isSneaking()) {
                // 1. Read how much XP we already have stored
                int xp = getStoredXp();
    
                // 2. Give all the XP to the player
                event.getPlayer().giveExp(xp);
    
                // 3. Set the stored XP to 0
                setStoredXp(0);
            } else {
                // 1. Read how much XP we already have stored
                int xp = getStoredXp();
    
                // 2. Figure out how much XP we need to take to get to `xpCapacity`
                int extraXpNeeded = xpCapacity - xp;
    
                // 3. Take as much XP from the player as we can to get there
                int xpToTake = Math.min(event.getPlayer().calculateTotalExperiencePoints(), extraXpNeeded);
                event.getPlayer().giveExp(-xpToTake);
    
                // 4. Set the new stored XP amount
                setStoredXp(xp + xpToTake);
            }
        }
    
        public void setStoredXp(int xp) {
            getStack().editPersistentDataContainer(pdc -> pdc.set(
                    STORED_XP_KEY,
                    PylonSerializers.INTEGER,
                    xp
            ));
        }
    
        public int getStoredXp() {
            return getStack().getPersistentDataContainer().get(
                    STORED_XP_KEY,
                    PylonSerializers.INTEGER
            );
        }
    }
    ```
=== "Kotlin"
    ```kotlin title="BaguetteOfWisdom.kt"
    class BaguetteOfWisdom(stack: ItemStack) : PylonItem(stack), PylonInteractor {
        companion object {
            val STORED_XP_KEY = NamespacedKey(MyAddon.getInstance(), "stored_xp")
        }

        private val xpCapacity = settings.getOrThrow("xp-capacity", Int::class.java)

        override fun getPlaceholders() =
            listOf(
                PylonArgument.of("xp_capacity", UnitFormat.EXPERIENCE.format(xpCapacity)),
                PylonArgument.of("stored_xp", UnitFormat.EXPERIENCE.format(getStoredXp()))
            )

        override fun onUsedToRightClick(event: PlayerInteractEvent) {
            if (event.player.isSneaking) {
                // 1. Read how much XP we already have stored
                val xp = storedXp

                // 2. Give all the XP to the player
                event.player.giveExp(xp)

                // 3. Set the stored XP to 0
                storedXp = 0
            } else {
                // 1. Read how much XP we already have stored
                val xp = storedXp

                // 2. Figure out how much XP we need to take to get to `xpCapacity`
                val extraXpNeeded = xpCapacity - xp

                // 3. Take as much XP from the player as we can to get there
                val xpToTake = min(event.player.calculateTotalExperiencePoints(), extraXpNeeded)
                event.player.giveExp(-xpToTake)

                // 4. Set the new stored XP amount
                storedXp = xp + xpToTake
            }
        }

        var storedXp: Int
            get() = stack.persistentDataContainer.get(
                NamespacedKey(MyAddon.instance, "stored_xp"),
                PylonSerializers.INTEGER
            )!!
            set(value) {
                stack.editPersistentDataContainer { pdc ->
                    pdc.set(
                        NamespacedKey(MyAddon.instance, "stored_xp"),
                        PylonSerializers.INTEGER,
                        value
                    )
                }
            }
    }
    ```

```yaml title="en.yml"
item:
  baguette_of_wisdom:
    name: "Baguette of Wisdom"
    lore: |-
      <arrow> Use the power of baguettes to transfer XP
      <arrow> <insn>Right click</insn> to charge with XP
      <arrow> <insn>Shift right click</insn> to discharge stored XP
      <arrow> <attr>XP capacity:</attr> %xp_capacity%
      <arrow> <attr>Stored XP:</attr> %stored_xp%
```
