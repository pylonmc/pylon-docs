# 新增自訂物品（Adding a custom item）

## 概述（Overview）

到目前為止，我們所建立的「自訂」物品，只是將法國麵包恢復飢餓值從 5 提升到 6。  
但如果我們希望能夠右鍵點擊生物讓它著火該怎麼辦？  
這不像食物那樣有現成的方法可用，因此我們需要撰寫一些程式碼來實現這個功能。

---

## 法國麵包火焰噴射器（The baguette flamethrower）

為了示範這一點，讓我們建立一個新的物品：「法國麵包火焰噴射器」。

### 建立「一般物品」（Creating a 'normal item'）

首先，我們先建立一個「一般」物品，就像前一章所做的那樣。

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
      <arrow> 使用法國麵包的力量點燃你所注視的方塊
```

---

### 建立自訂物品類別（Creating a custom item class）

接下來，我們要新增讓實體著火的程式碼。

為了做到這點，我們可以建立一個自訂類別 `BaguetteFlamethrower`。  
所有 Pylon 物品類別都必須繼承 [PylonItem]。

=== "Java"
建立一個新檔案 `BaguetteFlamethrower.java` 並加入以下內容：

```java title="BaguetteFlamethrower.java"
public class BaguetteFlamethrower extends PylonItem {
    public BaguetteFlamethrower(@NotNull ItemStack stack) {
        super(stack);
    }
}
```
=== "Kotlin"
建立一個新檔案 `BaguetteFlamethrower.kt` 並加入以下內容：

```kotlin title="BaguetteFlamethrower.kt"
class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack)
```

---

現在我們希望當玩家手持「法國麵包火焰噴射器」右鍵點擊實體時能發生事件。  
為了實現這點，我們可以實作 [PylonItemEntityInteractor] 介面。  
這是 Pylon 內建的一個介面，包含一個方法：`onUsedToRightClickEntity`。

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

---

### 使用自訂物品類別（Using the custom item class）

要讓這個類別生效，我們必須告訴 Pylon 使用此類別，而非預設的 `PylonItem`。

請將你的 `PylonItem.register(...)` 改為以下內容：

=== "Java"
```java
PylonItem.register(BaguetteFlamethrower.class, baguette);
```
=== "Kotlin"
```kotlin
PylonItem.register<BaguetteFlamethrower>(baguette)
```

---

就這樣！現在啟動伺服器，  
當你用法國麵包火焰噴射器右鍵點擊一個實體時，它將會著火 40 tick！

---

[PylonItem]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/PylonItem.html  
[PylonItemEntityInteractor]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/base/PylonItemEntityInteractor.html  
