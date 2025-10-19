# 新增物品（Adding an item）

## 概述（Overview）

到目前為止，我們的插件只有一個類別：`MyAddon`（或你改的名稱）。  
這個類別繼承了 [JavaPlugin] 並實作 [PylonAddon]。  
在類別中有一些註解說明各部分的功能，請先閱讀並了解它的運作方式。  
目前插件實際上還沒做任何事——所以讓我們來新增一個物品吧！

我們先來製作一個可恢復 6 格飢餓值的法國麵包（baguette）。

要建立一個簡單的物品，我們只需要兩樣東西：  
**物品的 key** 與 **物品堆疊（item stack）**。

---

## 新增物品（Adding the item）

### 建立 key（Creating a key）

[NamespacedKey] 是 Pylon 用來識別自訂物品、方塊、研究、實體等內容的方式。

!!! question "什麼是 NamespacedKey？為什麼要使用它？"
    key 其實就是一段文字，例如 `pylonbase:copper_dust`，讓 Pylon 能唯一識別你的物品。這類似於原版 Minecraft 的物品 ID。  
    為什麼不直接用 `copper_dust` 呢？因為如果有兩個外掛都新增了同名物品，我們就無法區分它們！  
    為了解決這個問題，Pylon 使用 [NamespacedKey]，也就是將「外掛名稱」與「物品名稱」結合，例如：`my_addon:copper_dust`。

在 `onEnable` 方法中建立一個新的 [NamespacedKey]：
=== "Java"
    ```java
    NamespacedKey baguetteKey = new NamespacedKey(this, "baguette");
    ```
=== "Kotlin"
    ```kotlin
    val baguetteKey = NamespacedKey(this, "baguette")
    ```

---

### 建立物品堆疊（Creating the item stack）

接著我們需要實際的物品。  
這裡會使用 [ItemStackBuilder]。

[ItemStackBuilder] 提供多種方法協助建立 [ItemStack]。  
例如 `.set(<component>, <value>)` 可設定物品屬性，如附魔、是否不可破壞等。

**當你建立 Pylon 物品時，務必使用 `ItemStackBuilder.pylonItem(<material>, <key>)`。**  
雖然有其他方式建立 [ItemStack]，但請**不要**用那些方法建立 Pylon 物品。

??? question "為什麼要用 `ItemStackBuilder.pylonItem`，而不是其他方式建立 [ItemStack]？"
    在底層，Pylon 會將物品的 key 儲存在 [PersistentDataContainer]（PDC）中。  
    當你使用 `ItemStackBuilder.pylonItem` 並提供 key 時，Pylon 會自動將 key 寫入該物品的 PDC。  
    若你自行建立 ItemStack，PDC 中將不含此 key，Pylon 就無法辨識該物品。  

    此外，[ItemStackBuilder] 也會自動設定物品的名稱與敘述（lore），  對應到預設的翻譯 key（後續章節會詳細說明）。

建立一個法國麵包的程式如下：
=== "Java"
    ```java
    ItemStack baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
            .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
            .build();
    ```
=== "Kotlin"
    ```kotlin
    val baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
        .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
        .build()
    ```

!!! info "Data components"
    Data component 是用來描述物品的資料結構，例如：
    - 「這是食物，能恢復 6 飢餓值」
    - 「這是鎬子，能以特定速度破壞方塊」  
    你可以在 [這裡](https://jd.papermc.io/paper/1.21.8/io/papermc/paper/datacomponent/DataComponentTypes.html) 查看完整列表。

---

### 註冊物品（Registering the item）

接下來我們需要將物品註冊進 Pylon。  
這需要兩個參數：**物品堆疊**與**代表該物品的類別**。  
稍後我們會介紹如何建立自訂物品類別，  目前可先使用預設的 [PylonItem] 類別：

=== "Java"
    ```java
    PylonItem.register(PylonItem.class, baguette);
    ```
=== "Kotlin"
    ```kotlin
    PylonItem.register<PylonItem>(baguette)
    ```

---

### 新增到 Pylon 指南（Adding the item to the guide）

最後，我們希望這個物品能出現在 Pylon 指南中。  
讓我們把它加到「食物（food）」分類中：

=== "Java"
    ```java
    BasePages.FOOD.addItem(baguetteKey);
    ```
=== "Kotlin"
    ```kotlin
    BasePages.FOOD.addItem(baguetteKey)
    ```

---

## 整合所有內容（Putting it all together）

以下是完整的程式碼：

=== "Java"
    ```java title="MyAddon.java" hl_lines="9-14"
        // Called when our plugin is enabled
        @Override
        public void onEnable() {
            instance = this;
    
            // Every Pylon addon must call this BEFORE doing anything Pylon-related
            registerWithPylon();
    
            NamespacedKey baguetteKey = new NamespacedKey(this, "baguette");
            ItemStack baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
                    .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
                    .build();
            PylonItem.register(PylonItem.class, baguette);
            BasePages.FOOD.addItem(baguetteKey);
        }
    ```
=== "Kotlin"
    ```kotlin title="MyAddon.kt" hl_lines="8-13"
        // Called when our plugin is enabled
        override fun onEnable() {
            instance = this
    
            // Every Pylon addon must call this BEFORE doing anything Pylon-related
            registerWithPylon()
    
            val baguetteKey = NamespacedKey(this, "baguette")
            val baguette = ItemStackBuilder.pylonItem(Material.BREAD, baguetteKey)
                .set(DataComponentTypes.FOOD, FoodProperties.food().nutrition(6))
                .build()
            PylonItem.register<PylonItem>(baguette)
            BasePages.FOOD.addItem(baguetteKey)
        }
    ```

現在就可以進遊戲測試看看了！

---

[JavaPlugin]: https://jd.papermc.io/paper/1.21.8/org/bukkit/plugin/java/JavaPlugin.html  
[PylonAddon]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/addon/PylonAddon.html  
[NamespacedKey]: https://jd.papermc.io/paper/1.21.8/org/bukkit/NamespacedKey.html  
[ItemStackBuilder]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/builder/ItemStackBuilder.html  
[ItemStack]: https://jd.papermc.io/paper/1.21.8/org/bukkit/inventory/ItemStack.html  
[PylonItem]: https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/item/PylonItem.html  
[PersistentDataContainer]: https://jd.papermc.io/paper/1.21.8/org/bukkit/persistence/PersistentDataContainer.html  
