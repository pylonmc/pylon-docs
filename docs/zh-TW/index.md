Pylon 是一個**即將推出**的 Minecraft Java 插件，它將大幅擴展原版遊戲的內容，包含電力機械、巨型多方塊結構、完整的流體系統、複雜的冶煉系統、廣泛的自動化選項、研究系統等更多功能。它的目標是取代 Slimefun。

Pylon 採用插件系統，這意味著任何人都可以撰寫外掛為 Pylon 添加內容！此外，它還具備多項實用特性，例如：

- 一流的翻譯支援，這意味著每位玩家選擇自己的語言。
- 完整的設定選項，包括每台機器的配置。
- 直覺且易於使用的指南，協助玩家了解插件。

## :frame_photo: Pylon 圖片展示（目前為止）

![Pylon 流體系統示意(A Pylon fluid setup)](img/fluid-setup.png)
![在 Pylon 指南中懸停於研究包上(Hovering over research pack in Pylon guide)](img/hovering-over-research-pack.png)
![液壓流體系統(Hydraulic fluid setup)](img/hydraulic-fluid-setup.png)
![銅製流體槽(Copper fluid tank)](img/looking-at-copper-fluid-tank.png)
![Pylon 指南中的研究畫面(Pylon research in the guide)](img/looking-at-research.png)
![醫療包介面(Medkit in guide)](img/medkit.png)
![放置銅管(Placing copper pipes)](img/placing-pipes.png)
![淨化塔設定介面(Purification tower config)](img/purification-tower-config.png)
![在 Pylon 指南中搜尋物品(Searching items in the Pylon guide)](img/searching-items.png)
![使用液壓磨輪轉動器(Using the hydraulic grindstone turner)](img/using-grindstone-turner.png)
![使用魔法祭壇(Using the magic altar)](img/using-magic-altar.png)
![使用冶煉爐(Using the smeltery)](img/using-smeltery.png)

## :stopwatch: 效能與穩定性

我們自第一天起便以效能與穩定性為首要考量：

- Pylon **廣泛的** 使用快取，並將大多數高負載系統以非同步方式運行，同時利用現代併行與效能特性（例如 coroutines）。 
- 此外，插件還提供多種效能調整選項——包括每台機器的更新頻率、限制玩家／區塊的機器數量、流體與能量的更新速率等。 
- Pylon 的設計最大程度地降低了資料損壞的風險，並包含多層錯誤處理機制以應對問題。  

注意：Pylon 可能無法完全與基岩版（Bedrock）相容。

## :calendar: 預定時程

**2025 年 9～10 月** — 限邀制 Alpha 測試開始。

**2025 年 11～12 月** — 開放式 Alpha 測試開始（預計在 MetaMechanists 伺服器上舉行）。  
我們預計會進行多輪為期數週的 Pylon 測試，用以修正錯誤、測試效能、提升穩定性與使用者體驗，確保插件正式發布時已經完善。

**2026 年初～中期** — Pylon 正式發布。

## :keyboard: 開發 Pylon 外掛

我們致力於讓 Pylon 的外掛開發變得簡單、直覺、靈活且有趣。  
從數百小時的 Slimefun 外掛開發經驗中所學到的教訓，使 Pylon 的 API 更加友好、清晰且彈性十足。  
Pylon 也完全支援使用 Kotlin 撰寫外掛，這比 Java 更簡潔且易於維護。

目前由於 Pylon 仍處於快速變動階段，外掛開發尚未開放，且暫缺高層級開發文件。  
我們計畫不久後推出完整的外掛開發指南，詳細介紹如何建立外掛及運用 Pylon 的各種系統，敬請期待！

## :link: 相關連結

Discord 邀請連結：[https://discord.gg/4tMAnBAacW](https://discord.gg/4tMAnBAacW)

Github 專案頁面：[https://github.com/pylonmc](https://github.com/pylonmc)

文件網站（**施工中**）：[https://pylonmc.github.io/](https://pylonmc.github.io/)

## :detective: 開發團隊

目前 Pylon 的核心開發團隊為：

@ohmvir 🇨🇦 — 來自 MetaMechanists 的新血開發者，雖然剛接觸插件開發，但表現出色，快速上手並新增了許多基礎內容，如生命護符與斬首之劍，同時協助處理各類任務。

@overlordidra 🇬🇧 — MetaMechanists（知名 Slimefun 伺服器）經營者超過四年，亦為 Quaptics 的開發者。  
他負責了許多核心系統，包含 Pylon 指南、流體系統、液壓系統、自動測試代碼，以及自訂方塊／實體／物品追蹤系統等。

@seggan 🇺🇸 — 資深 Slimefun 外掛開發者，作品包括 SlimefunWarfare、SFCalc，以及知名的 Galactifun 外掛。  
他同時也對其他外掛、Paper 伺服器軟體及 Slimefun 本體有貢獻。  
Seggan 負責許多核心系統，包括完整翻譯系統、WAILA、研究系統、內部登錄系統與配方系統（以及其他眾多功能！）。

我們同時感謝其他協助成員：

@ihateblueb — 曾經營 Slimefun 伺服器 Orchid，目前協助新增更多內容（例如電梯系統由她製作！）。

@justahuman_xd — 負責許多技術層面的功能，如方塊與盔甲材質系統，擁有豐富的 Slimefun 開發經驗，並提供了寶貴建議。

@.ph.enix — 曾負責我們的 CI 系統，設立自動測試與版本發布流程。雖然他已離開專案，但我們非常感謝他的貢獻。

@vaan1310 — 協助修復錯誤、實作資料驅動研究功能，並協助審查 Pull Request。

如果你有興趣參與開發，歡迎加入我們的 Discord！  
不需要是專家，只要具備基本插件開發經驗即可。  
我們有各種不同難度的任務，從簡單到極具挑戰性，讓我們幫你找到合適的工作項目。

## :question: 有問題嗎？

歡迎在 Discord 伺服器留言，我們將樂於回覆。
