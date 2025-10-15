# 實作練習(Practice tasks)

### 任務 1(Task 1)

修改法棍火焰噴射器，使其同時對目標實體召喚閃電。新增一個設定值 `strike-with-lightning`，可為 `true` 或 `false`，用以控制是否對目標實體召喚閃電。

??? tip "提示"
    [https://jd.papermc.io/paper/1.21.8/org/bukkit/World.html#strikeLightning(org.bukkit.Location)](https://jd.papermc.io/paper/1.21.8/org/bukkit/World.html#strikeLightning(org.bukkit.Location))

### 任務 2(Task 2)

建立兩個版本的法棍火焰噴射器：一個會召喚閃電（稱為「宙斯法棍火焰噴射器」），另一個不會（一般的「法棍火焰噴射器」）。

### 任務 3(Task 3)

建立「至高智慧法棍」（Baguette of Supreme Wisdom），可儲存最多 1000 經驗值，同時保留原本的「智慧法棍」。

### 任務 4(Task 4)

為「智慧法棍」新增一個 `efficiency`（效率）設定值。例如設定為 0.8 時，在釋放經驗值時僅能取回 80% 的經驗值。記得在說明文字（lore）中加入顯示，並建立對應的佔位符（placeholder）！

### 任務 5(Task 5)

建立一個新物品：「神聖審判法棍」（Baguette of Divine Judgement）。 

此物品應與智慧法棍一樣可儲存經驗值，但當玩家按住 Shift + 右鍵點擊時，不是釋放經驗值，而是消耗儲存的經驗值在玩家注視的方塊上召喚閃電。所需的經驗值應可透過設定調整，並在說明文字中顯示。

### 任務 6(Task 6)

建立一個新物品：「忠誠法棍」（Baguette of Loyalty）。當玩家按住 Shift + 右鍵點擊時，此物品會綁定到該名玩家，並記住被綁定者。若其他人嘗試再次綁定，將會被閃電擊中。 

當右鍵點擊時，此法棍僅會治癒與其綁定的玩家。

治癒量應可透過設定調整，並在說明文字中顯示治癒量與綁定玩家的名稱。

(這項任務比其他任務稍難，且有多種實作方式。)

??? tip "提示"
    你不能直接將玩家物件儲存在 PDC 中，但可以儲存玩家的 UUID。
