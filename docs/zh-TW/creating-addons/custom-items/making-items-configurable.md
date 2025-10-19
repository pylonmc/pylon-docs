# 讓物品可設定

## 概述

讓我們新增一個設定檔，讓伺服器擁有者能夠調整法棍火焰噴射器點燃實體的時間長度。

---

## 建立設定檔

如果你查看伺服器的 Pylon 設定目錄 (`run/plugins/PylonCore/settings/pylonbase`) 你會發現每個物品與方塊都有各自的設定檔。

例如， `bandage.yml` contains:

```yaml title="bandage.yml"
consume-seconds: 1.25
heal-amount: 4.0
```

我們想要新增自己的設定檔，讓你可以選擇法棍火焰噴射器點燃實體的時間長度。

建立一個新檔案 `resources/settings/baguette_flamethrower.yml` 並加入以下內容：

```yaml title="baguette_flamethrower.yml"
burn-time-ticks: 40
```

!!! success "最佳實踐"
    當你的設定項目代表一個數值時，請在名稱中包含單位。 如果我們只將其命名為 `burn-time`, 使用者可能不知道該值的單位是 tick，並誤以為是秒或其他單位。

Pylon 會自動將你的所有設定檔複製到 `run/plugins/PylonCore/settings/<your-addon-name>` 當設定檔首次被使用時。

---

## 使用設定檔

要讀取 `burn-time-ticks` 值，我們可以使用 `getSettings().getOrThrow(...)`:

=== "Java"
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
    !!! question "Pylon 如何知道要使用哪個設定檔？"
        設定檔實際上是依照 **key** 分別設定的，而不是依照物品本身。 當呼叫 `getSettings()`, 它只是根據物品的 key 尋找對應的設定檔！ 這只是 `Settings.get(getKey())`. 如果你使用 `Settings.get(new NamespacedKey(MyAddon.getInstance(), "buffoon"))` 那麼 `buffoon.yml` 設定檔就會被讀取。
=== "Kotlin"
    ```kotlin title="BaguetteFlamethrower.kt" hl_lines="2"
    class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
        private val burnTimeTicks = settings.getOrThrow("burn-time-ticks", Int::class.java)
    
        override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
            event.rightClicked.fireTicks = 40
        }
    }
    ```
    !!! question "Pylon 如何知道要使用哪個設定檔？"
        設定檔實際上是依照 **key** 分別設定的，而不是依照物品本身。 When accessing `settings`, 它只是根據物品的 key 尋找對應的設定檔！ 這只是 `Settings.get(key)`. 如果你使用 `Settings.get(NamespacedKey(MyAddon.instance, "buffoon"))` 那麼 `buffoon.yml` 設定檔就會被讀取。

!!! question "為什麼我們使用 `getOrThrow` 而不是 `get`？"
    Settings 也有一個 `get` 方法。 這個方法在找不到 key 時只會回傳 null， 因此僅應在不一定需要該 key 的情況下使用。 如果使用 `getOrThrow`，當缺少 key 時會丟出清晰的例外，並包含缺少的 key 與位置資訊。

現在我們就可以使用該設定值來點燃實體了！

=== "Java"
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
=== "Kotlin"
    ```kotlin title="BaguetteFlamethrower.kt" hl_lines="5"
    class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
        private val burnTimeTicks = settings.getOrThrow("burn-time-ticks", Int::class.java)
    
        override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
            event.rightClicked.fireTicks = burnTimeTicks
        }
    }
    ```

試著更改設定值，燃燒時間也會隨之改變。

!!! danger
    執行伺服器任務時，會刪除 `plugins` 資料夾內的所有內容， 意味著你在那裡修改的設定檔將會被覆蓋。 建議你直接修改預設值，或手動啟動伺服器，以避免在重啟時刪除 `plugins` 資料夾。
