# 開始使用

Pylon Core 是以 [Kotlin](https://kotlinlang.org/) 編寫的，一種與 Java 相似但具有更多現代化特性與簡潔語法的語言。  
如果你熟悉 Java，將能很快上手 Kotlin。

Pylon Base 則是以 Java 編寫。

## 如何開始

1. 複製 `pylon` 儲存庫：`git clone https://github.com/pylonmc/pylon`（或使用像 GitHub Desktop 這樣的圖形介面）
2. 若你使用 IntelliJ，它會自動完成所有設定。  
   若否，請執行 `./gradlew`。這會自動複製 `pylon-core` 與 `pylon-base` 儲存庫。
3. 如果你想將修改提交到 Pylon 專案，  
   **請刪除 `pylon-core` 或 `pylon-base` 目錄（視你要貢獻的部分而定），接著 fork 該儲存庫並將你的 fork 複製回同一個目錄中。**  
   否則，你將無法提交 Pull Request（除非你是 Pylon 開發者並擁有該專案的存取權）。

更多資訊請參考 [Pylon Master Project](./master-project) 頁面。

## 提交貢獻

我們歡迎對 Core 與 Base 的貢獻，但若你計畫進行重大變更，建議先與 Pylon 團隊確認，因為我們可能已有既定規劃，未必與你的修改相容。  
如果你有興趣參與較大型的開發或有任何疑問，請加入我們的 Discord 伺服器與我們討論 :)

完成修改後，請開啟 Pull Request，並簡要說明你做了哪些變更以及原因。

## 測試

Pylon Core 擁有一組整合測試。  
測試應僅針對關鍵功能（例如方塊儲存與配方）新增。

## 自訂 Dokka

Pylon 使用自訂版本的 Dokka 來生成 Javadoc。  
這是因為預設的 Dokka 輸出存在許多錯誤，且外觀不佳。  
Seggan 已經向 Dokka 專案提交修正的 Pull Request，但尚未被合併，因此暫時採用自訂版本。

若你希望查看「修正版」的文件輸出，可依以下步驟操作：

1. 複製 `pylonmc/dokka` 儲存庫：`git clone https://github.com/pylonmc/dokka`
2. 切換至 `pylon` 分支：`git checkout pylon`
3. 在根目錄中執行：  
   `./gradlew publishToMavenLocal -Pversion=2.1.0-pylon-SNAPSHOT`  
   注意：Dokka 專案相當龐大，首次建置將花費較長時間。  
   以 Seggan 的筆電為例，第一次執行約需 10 分鐘。  
   後續建置將會更快，只要不刪除快取即可。
4. 現在，在 Pylon 主專案中執行：  
   `./gradlew :pylon-core:pylon-core:dokkaGenerate -PusePylonDokka=true`  
   生成的輸出會位於：  
   `pylon/pylon-core/pylon-core/build/dokka`

## 卡關了，該怎麼辦？

1. 若是與 Pylon 相關的問題，先查看文件中是否已有說明。  
   若非 Pylon 特有問題，請善用 Google 搜尋。
2. 在相關儲存庫的 Issues 中搜尋是否已有類似問題。
3. 在我們的 Discord 伺服器中搜尋相關關鍵字，看看是否已有討論。
4. 若仍無法解決，請在 Discord 伺服器中發問。

[comment]: <> (TODO: 讓這份說明更易理解，也許可以加入截圖等輔助內容，因為經驗較少的使用者可能完全看不懂這些指令在做什麼)
