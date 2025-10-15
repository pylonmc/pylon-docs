# Pylon 主專案

Pylon 有一個主儲存庫（master repository），其中包含 `pylon-core` 與 `pylon-base`。  
這樣的架構讓你能夠在自己的環境中運行自製版本的 Core，  
使測試新功能變得更加容易。  
這正是「如何開始」章節中所使用的方式。  
我們建議你透過主儲存庫同時對 Base 與 Core 進行修改，  
本指南後續的內容也會假設你是以這種方式進行開發。

## 專案結構
主專案的結構如下：
```
pylon/
    pylon-base/
    pylon-core/
        dokka-plugin/
        nms/
        pylon-core/
        test/
```
`pylon-base` 包含了 Pylon 的 Base 外掛。  
`pylon-core` 則包含四個子專案：`dokka-plugin`、`nms`、`pylon-core` 與 `test`。  
`dokka-plugin` 儲存我們自訂的 Dokka 插件，用於協助格式化 Javadocs。  
`nms` 包含所有與伺服器內部機制（server internals）互動的 Pylon Core 程式碼。  
它被分離為獨立的子專案，目的是將潛在不穩定的程式碼與其他部分隔離開來。  
`pylon-core` 包含主要的 Pylon Core 程式碼，`test` 則包含 Pylon Core 的整合測試。

## 任務（Tasks）
Pylon 主專案中包含了一些在開發時非常有用的任務：

| 任務名稱                     | 別名（Alias）        | 說明                                                                                                     |
|------------------------------|---------------------|----------------------------------------------------------------------------------------------------------|
| `runServer`                  | `runSnapshotServer` | 使用目前版本的 Pylon Base 與 Pylon Core 啟動 Minecraft 伺服器                                           |
| `:pylon-base:runServer`      | `runStableServer`   | 使用最新穩定版本的 Pylon Core 及目前版本的 Pylon Base 啟動 Minecraft 伺服器                             |
| `:pylon-core:test:runServer` | `runLiveTests`      | 執行 Pylon Core 的整合測試                                                                               |

!!! danger
    若你在 IntelliJ 中使用這些任務的別名啟動並附加除錯器，你會發現它無法運作。  
    我也不知道為什麼會發生這種情況。  
    若要成功附加除錯器，請執行實際的任務名稱而非別名。  
    例如：不要執行 `runSnapshotServer`，請執行 `runServer`。
