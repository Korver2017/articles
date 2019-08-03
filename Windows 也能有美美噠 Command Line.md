![](https://images.unsplash.com/photo-1526045405698-cf8b8acc4aaf?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1351&q=80)

Photo by [freestocks.org](http://freestocks.org/) on Unsplash

## 謝謝老闆（擠）🙏 / 最初是拳 👊

感恩我們家老大配給筆電，藉由再次設定 Cmder 的過程，把過去的筆記撈出來並且 Run 過一次，感謝老大五倍恩寵！（？

許久以前在看 Git 的線上課程時，因為課程講師是使用 Mac 系列，又加上套用了佈景主題，所以一時讓我覺得異常興奮！這跟我印象中只有黑底白字的 Command Line / Terminal 完全不一樣啊啊啊...

但當時滿腔熱血的我，最後卻是得到意外的訊息...Windows 在這個區塊似乎不太能施展手腳啊 Q_Q

登楞！因此我就開始由愛生恨...（x

## Cmder

身為一個 Windows 的使用者，輾轉仍然是接觸到了比較有「溫度」（保哥說的 🤣）的 Command Line - **Cmder。**

當然，我認為 Cmder 已經比最初黑底白字的 Command Line 用起來心情好很多了（？） 但心中仍然是嚮往當初印象中 Mac 的 Terminal 樣式。咳咳...（清嗓） 說真的，絕對不是因為我對 Mac 的忌妒、羨慕或迷戀（XD）就是希望看看能不能有更美觀的工具使用。

## 從 Cmder 到美美噠 Cmder

一開始用 Cmder 的時候有稍微 Survey 一下，看有沒有可以套用或改變樣式的佈景主題。不過不知道是不是下不對關鍵字還是怎麼樣...總之最後是不了了之了 XD

言歸正傳，最後我是取用這邊的資源：

GitHub: [https://github.com/AmrEldib/cmder-powerline-prompt](https://github.com/AmrEldib/cmder-powerline-prompt)

當然他已經有教學了，我在這裡用中文簡易的走過一下。

## STEP 1. Download ZIP

Download ZIP 後解壓縮，找到當中的 5 個 `.lua` 檔； `powerline_core.lua` 、 `powerline_git.lua` 、 `powerline_hg.lua` 、 `powerline_npm.lua` 、 `powerline_prompt.lua` 。

## STEP 2. 增加至設定

把 5 個 `.lua` 檔複製到 `..\cmder\config` ，重開 Cmder 後可以看到樣式的改變。

![](/images/cmder_original.png)

載入 .lua 檔之前

![](/images/cmder_lua.png)

更新樣式後

![](/images/cmder_lua_project.png)

進入專案與顯示分支樣式

## STEP 3. 下載並安裝 Fira Code 字型檔

GitHub Source: [https://github.com/tonsky/FiraCode/releases](https://github.com/tonsky/FiraCode/releases)

## STEP 4. 更改字型

開啟 Cmder 並鍵入 `Alt + Win + p` 開啟設定介面（Settings），接著就可以在 `Fonts` 選擇更改字型，選取 `Fira Code`。

![](/images/settings.png)

## STEP 5. 恭喜完成 👏🎉

這樣就能看到分支名稱（master）旁邊的圖案了！

![](/images/before_firacode.png)

套用 Fira Code 之前

![](/images/after_firacode.png)

套用 Fira Code 後即可顯示圖樣

## 備註：

我用的 Color Scheme 是 `Ubuntu` 。

## XML 的佈景主題解決方案 🐼

之前搜尋的時候也看到了這個 Logo 很漂亮（？）的佈景主題，是用 `.xml` 的方式載入。一樣在 GitHub 上面有介紹如何安裝，我用中文快速導覽。

GitHub: [https://github.com/HamidFaraji/panda-theme-cmder](https://github.com/HamidFaraji/panda-theme-cmder)

![](/images/panda_logo.png)

Photo from [https://github.com/HamidFaraji/panda-theme-cmder](https://github.com/HamidFaraji/panda-theme-cmder)

## STEP 1. Download ZIP

Source 同 GitHub: [https://github.com/HamidFaraji/panda-theme-cmder](https://github.com/HamidFaraji/panda-theme-cmder)

## STEP 2. 開啟 Cmder Settings

開啟 Cmder 並鍵入 `Alt + Win + p` 開啟設定介面。

## STEP 3. Import .xml File

點選 `Import...` 選項後找到下載的 `.xml` 檔，檔名為 `Panda-Theme-Cmder.xml` ，最後記得 `Save settings`。

![](/images/save_settings.png)

## STEP 4. 恭喜完成 👏🎊

![](/images/after_save_settings.png)

備註：

如果之前有載入 `.lua` 檔案的話，記得要移除一下，不然畫面可能會不如預期。

## 最初是拳；最後是結論 😈

說真的，這篇不是什麼特別的教學，純粹只是自己的經驗就分享一下。也感謝我們家老闆，鼓勵我參與各種 Conf、討論，最重要的是 **分享** 。看到我們家老大對 Opensource 的熱情（像是在筆電上 Opensource 的貼紙 😎），我著實是備受感染與激勵 💪

未來我也會陸續分享一些我的經驗或想法，可能不會是什麼深度教學。當然，可以的話我也會盡力貢獻。

不管怎麼樣，我現在就是陸續寫 Blog，養成分享的習慣，也從其中追求成長。如果您對文章有什麼想法，歡迎留下您的寶貴意見，甚至是分享其他資源，大家彼此多交流囉～ 😆