# 進階敘述（Advanced lore）

## 概述（Overview）

讓我們看看物品敘述還能做些什麼。現在的版本相當無聊：

![Boring baguette flamethrower lore](img/boring-baguette-flamethrower.png)

---

## Minimessage

敘述不只是純文字——它可以使用 **標籤（tags）**，例如 `<arrow>`、`<red>`、`<bold>`。  
這些標籤由 [MiniMessage](https://docs.advntr.dev/minimessage/index.html) 提供。  

!!! info
    你可以在 [這裡](https://docs.advntr.dev/minimessage/format.html) 查看完整的 MiniMessage 標籤清單。

以下是一些使用 minimessage 的範例：

### 基本顏色（Simple color）

```yaml title="en.yml"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of <red>baguettes</red> to ignite the entities you look at
```

![simple-color](img/simple-color.png)

### 十六進位顏色（Hex color）

```yaml title="en.yml"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of <#ff6200>baguettes</#ff6200> to ignite the entities you look at
```

![hex-color](img/hex-color.png)

### 漸層（Gradient）

```yaml title="en.yml"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of <gradient:#0055a4:white:#ef4135>baguettes</gradient> to ignite the entities you look at
```

![gradient](img/gradient.png)

### 格式化（Formatting）

```yaml title="en.yml"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the <underlined>power of <bold>baguettes</bold> to ignite</underlined> the entities you look at
```

![formatting](img/formatting.png)

!!! success "最佳實踐（Best practice）"
    **避免在物品名稱與敘述中使用過多顏色。**  
    理想情況下，你不應像上面範例那樣強調「baguette」，因為這沒有實際必要。

    雖然很容易想用顏色強調，但在 Pylon 中物品種類繁多，這樣會造成混亂！  
    建議只在**特別情況**下使用顏色或格式（粗體、斜體等）。  
    例如：放大鏡（Loupe）會用紅色標示「使用後該物品會被消耗」——這樣的警示才有意義。

---

## Pylon 的自訂標籤（Pylon's custom tags）

樂趣還沒結束——Pylon 也加入了自己的 MiniMessage 標籤！  
你已經見過 `<arrow>`，它在整個系統中非常常見。  
另外還有兩個非常重要的標籤：`<insn>`（指令）與 `<attr>`（屬性）。

!!! info
    你可以在 [這裡](TODO) 查看 Pylon 的自訂標籤完整列表。

### 指令（Instructions `<insn>`）

這個標籤只是快速標示特定顏色文字的捷徑，我們通常用它來表示**操作指令**：

```yaml title="en.yml" hl_lines="5"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of baguettes to ignite the entities you look at
    <arrow> <insn>Right click</insn> to ignite the entity you're looking at
```

![formatting](img/instruction.png)

### 屬性（Attributes `<attr>`）

這個標籤則用於標示物品屬性：

```yaml title="en.yml" hl_lines="6"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of baguettes to ignite the entities you look at
    <arrow> <insn>Right click</insn> to ignite the entity you're looking at
    <arrow> <attr>Burn time:</attr> 2 seconds
```

!!! success "最佳實踐（Best practice）"
    請依序排列：**描述 → 指令 → 屬性**，這樣可讓所有物品風格一致。

![formatting](img/attribute.png)

「但等一下！」你可能會說，「我們剛才不是設定了燃燒時間嗎？它不一定總是 2 秒啊！」

沒錯。這正是**占位符（placeholders）**登場的時候。

---

## 占位符（Placeholders）

有時候，我們需要從程式中傳遞變數到敘述中，例如燃燒時間。  
這可以透過占位符完成。占位符是像 `%burn-time%` 這樣的標記，代表「這裡會被替換成實際值」。

`PylonItem` 類別中有個方法 `getPlaceholders`，  
當你覆寫它時，可以回傳一個占位符清單，用於在敘述中替換內容。  
讓我們在 `BaguetteFlamethrower` 中實作這個方法：

=== "Java"
```java title="BaguetteFlamethrower.java" hl_lines="13-18"
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
                PylonArgument.of("burn-time", burnTimeTicks / 20.0)
        );
    }
}
```
=== "Kotlin"
```kotlin title="BaguetteFlamethrower.kt" hl_lines="8-9"
class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
    private val burnTimeTicks = settings.getOrThrow("burn-time-ticks", Int::class.java)

    override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
        event.rightClicked.fireTicks = burnTimeTicks
    }

    override fun getPlaceholders() =
        listOf(PylonArgument.of("burn-time", burnTimeTicks / 20.0))
}
```

現在我們就能在物品敘述中使用該占位符。  
占位符的語法是用 `%` 包住你設定的名稱，例如 `%burn-time%`：

```yaml title="en.yml" hl_lines="6"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of baguettes to ignite the entities you look at
    <arrow> <insn>Right click</insn> to ignite the entity you're looking at
    <arrow> <attr>Burn time:</attr> %burn-time% seconds
```

![formatting](img/placeholder.png)

!!! success "最佳實踐（Best practice）"
    **請永遠使用占位符而非硬編值（hardcoded values）**，  
    以確保敘述中顯示的數值永遠與實際一致。

---

### 單位（Units）

最後一件事。  
我們目前手動加上了「seconds」，但其實 Pylon 有一個「單位 API」可以自動處理。  
它會根據數值自動格式化單位，非常簡單好用：

=== "Java"
```java title="BaguetteFlamethrower.java" hl_lines="16"
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
```kotlin title="BaguetteFlamethrower.kt" hl_lines="9"
class BaguetteFlamethrower(stack: ItemStack) : PylonItem(stack), PylonItemEntityInteractor {
    private val burnTimeTicks = settings.getOrThrow("burn-time-ticks", Int::class.java)

    override fun onUsedToRightClickEntity(event: PlayerInteractEntityEvent) {
        event.rightClicked.fireTicks = burnTimeTicks
    }

    override fun getPlaceholders() =
        listOf(PylonArgument.of("burn-time", UnitFormat.SECONDS.format(burnTimeTicks / 20.0)))
}
```

```yaml title="en.yml" hl_lines="6"
baguette_flamethrower:
  name: "Baguette Flamethrower"
  lore: |-
    <arrow> Use the power of baguettes to ignite the entities you look at
    <arrow> <insn>Right click</insn> to ignite the entity you're looking at
    <arrow> <attr>Burn time:</attr> %burn-time%
```

![formatting](img/unit.png)

!!! info
    你可以在 [這裡](https://pylonmc.github.io/pylon-core/docs/javadoc/io/github/pylonmc/pylon/core/util/gui/unit/UnitFormat.html) 查看 Pylon 的預設單位清單。

!!! success "最佳實踐（Best practice）"
    **請使用單位 API，而非手動加上單位文字。**  
    這樣所有物品的單位都能保持一致，數值格式也更統一。  
    否則有時候可能會出現「2.0」或「2」這種差異。  
    使用單位 API 可以確保所有顯示格式都相同。
