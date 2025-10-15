# 安裝（Installation）

!!! danger
    **⚠️ PYLON 目前仍屬於實驗性階段。**  
    請僅在你「願意刪除」的測試伺服器上執行。  
    下一個版本的 Pylon **很可能與目前版本不相容**。  
    若你在正式環境安裝導致資料遺失，我們只會指著螢幕笑你 🤷‍♂️。

1. 確保你正在運行 **Paper** 或其分支。Pylon **不相容於 Spigot**。
2. 從 [這裡](https://github.com/pylonmc/pylon-core/releases) 下載最新版本的 **Pylon Core**。
3. 從 [這裡](https://github.com/pylonmc/pylon-base) 下載最新版本的 **Pylon Base**。
4. 將 `.jar` 檔案放入伺服器的 `plugins` 資料夾，然後**重新啟動伺服器**。  
   ⚠️ [請勿使用 /reload 指令](https://madelinemiller.dev/blog/problem-with-reload/)。  
   第一次啟動會比平常久，但之後的啟動速度會顯著提升。
5. 檢查 `Pylon Core` 與 `Pylon Base` 的外掛資料夾，了解可用的所有設定選項。
6. [安裝一些外掛吧。](list-of-addons.md)
7. 完成！

---

### Pylon 的資料儲存位置在哪裡？

你可能會注意到 Pylon 並沒有使用資料庫，  而且在插件資料夾中也找不到任何儲存檔案。  
這是因為 Pylon **將所有資料儲存在世界檔（world file）內部**，  與 Minecraft 自身儲存方塊與實體的方式相同！

因此，你只需要備份世界檔即可：  
**Pylon 的資料會永遠與世界資料保持一致。**

這也代表 Pylon **比其他類似外掛更不容易發生資料毀損**。
