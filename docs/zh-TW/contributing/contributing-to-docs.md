# 為文件作出貢獻

我們使用 [MkDocs](https://www.mkdocs.org/) 和 [Github Pages](https://pages.github.com/) 來建立並維護你現在正在閱讀的文件網站。

## 先決條件

在開始之前，請確保你的系統已安裝以下內容：

- **Python 3** - MkDocs 所需
- **pip** - Python 套件安裝工具（通常隨 Python 一起提供）

請參考 [MkDocs 的安裝指南](https://www.mkdocs.org/user-guide/installation/) 了解如何安裝這些相依套件。

## 如何開始

1. 複製 `pylon-docs` 儲存庫：`git clone https://github.com/pylonmc/pylon-docs`
2. 安裝所有必要的相依套件：`pip install -r requirements.txt`
3. 使用下列指令在本機執行文件網站：`mkdocs serve`

## 部署

只有核心成員可以部署網站。

1. 複製 `pylonmc.github.io` 儲存庫：`git clone https://github.com/pylonmc/pylonmc.github.io`
2. 在 **pylonmc.github.io 儲存庫** 中執行以下指令以部署網站：  
   `mkdocs gh-deploy --config-file ../pylon-docs/mkdocs.yml --remote-branch master`

[comment]: <> (TODO: 添加更詳細的說明，例如 Slimefun 的 (https://github.com/Slimefun/Slimefun4/wiki/Expanding-the-Wiki))
