# Modern Web 2019 偽遊記 x Functional Programming x 抽象化

![](/images/functional_programming/cover.png)
Photo by [Andrew Schultz](https://unsplash.com/@andrewschultz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

## 最初是拳 👊

呃‧‧‧這個偽遊記應該早就要寫出來給公司老大聞香的‧‧‧而且是打算從 Opening 開始做連載。

但一陣子以來因為公司專案比較忙，所以一直沒空開始著手‧‧‧（被毆。無奈時間實在是拖太久了，所以決定先從最期待分享的議程開始著眼寫起。

‧‧‧話說這樣，就不用交給老大的孫子燒給他了（又被毆 XD。

## 🐾 關於這篇偽遊記

1. 本文對照議程：Abstract Thinking─從 Functional Programming 看見程式之美；By 洪名辰（Jerry）。

2. 文中會帶到講者所分享的內容，但不會牽著你的手舊地重遊（x。

3. 分享個人所見所聞、心得、收穫等。

## 🐾 寫程式與抽象化

在寫程式的路途上，就算我們已經能解決幾乎所有的問題與完成需求時，我們仍然不斷在「學習」寫程式；事實上我們在做的，是進一步的學習「如何封裝程式」，又或者說是「如何做好抽象化」。

依循脈絡，我們先來談談「抽象化」吧！

### 抽象化（Abstraction）

「抽象化」依據維基百科定義如下：

> 抽象化（英語：Abstraction）是指以縮減一個概念或是一個現象的資訊含量來將其廣義化（Generalization）的過程。

> 主要是為了只保存和一特定目的有關的資訊。例如，將一個皮製的足球抽象化成一個球，只保留一般球的屬性和行為等資訊。

Jerry 大提出的想法是：

> 抽象化就是把重複出現的模式或類似的事物作出歸納的過程。

前述維基百科舉了一個關於球的例子，講員則是提出了關於顏色的認知經驗。

假設今天你是一個寶寶（？，當媽媽告訴你香蕉是黃色的，身為寶寶的你可能會誤以為黃色就指的是香蕉；而將來的某一天媽媽又跟你說，計程車是黃色的。這時候你會很奇妙的在大腦內，重新認知黃色、香蕉，以及計程車，個別與彼此之間的關係。

> 這是人類與生俱來，學習事物的能力與天賦。

想想我們自己是怎麼學會某些技術的。

事實上，找出跨領域共同的成份內容、快速建立技術與技術間的連結，就能幫助我們快速學習新技術。比如說已經學會了 CSS，當遇到要學習 CSS Module 時，了解其間的 關聯性 與 差異性，就能進一步加速學習與理解。

那我們該怎麼做，如何幫助自己學習抽象化，進而在 Coding 時寫出更理想封裝的程式碼呢？接著就要講到今天的另一個主題； **Functional Programming（FP）**。

### Functional Programming

Functional Programming 的段落著重在兩個重點：

1. Function Composition。

2. 到處都是 `map`。

以下內容中有幾處，因為小弟我對於 Functional Programming 的認識尚淺，特別針對幾個名詞做了一些查詢、筆記。

### Function Composition

Function Composition；中文翻譯為 **合成函數 / 複合函數**。

> 逐點地把一個函數作用於另一個函數的結果，所得到的第三個函數。

好吧，有點拗口的文言文‧‧‧（？）讓我們來張極簡（又醜）圖示輔助一下。

![](/images/functional_programming/function_composition.png)Function Composition

由圖可知，合成函數 `h = g。f` ，藉由 `f` 與 `g` 這兩個函數合成而得。 `Input X` 藉由 `Function composition h` 得出 `Result Z`。

緊接著我們來看看為什麼「到處都是 `map`」。

### 到處都是 map

怎麼說「到處都是 `map`」呢？從一般可見的 `Array map`，以至於 `TypeScript`、`Haskell─Type Signature` 到 `Observable map` ‧‧‧等等，的確到處都是 `map`。

說到這，請容許我開一隻支線─**Functor & fmap**。

### Functor & fmap

什麼是 Functor？舉例而言像是 **Array**，它含有 `map ()` 屬性，所以可以稱為 Functor。而 Functor 的一大重要特性，要能確保資料是 **Immutable data**。

而這個 `map ()`，對於 Functor 來說，則進一步將這個行為進行規範，並稱之為 `fmap`。

這時再看看下圖，並不難發現與上一副圖兩者之間的異同；也就是說，我們可以抽象化來看 `fmap`。

![](/images/functional_programming/fmap.png)

### Function 也是 Functor

Function 其實也是 Functor，怎麼說呢？

![](/images/functional_programming/function_fmap.png)

![](/images/functional_programming/compose_function.png)

由上圖可知，Function 的 map 就是 `Compose Function`。

## 🐾 議程的最後

> 當我們學會了這些抽象化，再回過頭去學各個程式語言，會發現簡單很多。

> 學習好的抽象化可以幫助我們學習一個完全不同領域的知識。

咦！這說法怎麼讓人有種「第一性原理」的既視感（？）呃‧‧‧說說而已，因為兩者還是有很大的不同；但就結論而言，確實達到了很大程度雷同的「效果」。

也因為這個「效果」，講員在議程最後直接明示了「Learn How to Learn」這個近年火紅流行的思潮；也幾乎貫穿了整個議程的前後。

比較出乎意料的是，Jerry 大隨後又提出了一個進一步的想法─「Think How to Think」。

從相對既有討論「學習」這件事，延伸到「思考我們該如何思考」；甚至說是「思考我們該如何做抽象化」。因為「思考」、「抽象化」，並不只適用於「學習」而已，更可能直接關乎，如決策、人生規劃‧‧‧等等的更高層次。

![](/images/functional_programming/elon_musk.png)Elon Musk 曾以「第一性原理」詮釋自己的思維模式，使此理論爆紅再度躍升檯面

## 🐾 為何我選擇這場議程？

會選擇這場議程的主要原因如下：

1. 想學 **Abstract Thinking**。

2. 想學 **Functional Programming**。

（欸！是在供三小，跟沒說一樣啊‧‧‧ XD）

其實相關動機、背景是這樣的（清嗓。

曾經有機會跟公司老大討論寫程式、實踐功能的相關話題，他提到從得知、確認產品需求，到構想程式與架構，以至最後完成實踐與產出；就是不斷的在 **具體與抽象** 之間來回轉換的過程（在「有跟沒有」之間‧‧‧欸？）。

![](/images/functional_programming/between_exist_and_not.png)為了保護當事人，所以‧‧‧

稍微拉回來一點，當初討論最早還是專注在某個功能，該如何構想與完成；進而談到今天的主題─Abstract Thinking。

那 Functional Programming 呢？

### 老實說我什麼都想學

程式的世界真的很有趣，如此的引人入勝，讓人什麼都想了解、什麼都想學！

然而學海無涯。手邊存了很多資源，不同來源、不同主題。寫專案之餘，曾有機會好好沉澱下來思考，該怎麼規劃自己學習的 Roadmap 呢？

在參加這場議程之前，除了手邊正在看 OOA&D 的書，也有在考慮安排 Clean Code、Node.js、FP、TypeScript‧‧‧哦，對了！當然還包括一些程式架構之類的。

而在這場議程後，我想 Functional Programming 會拉到前面的位置，預計 OOA&D 看到比較後面時，會優先選擇 Functional Programming 投入。

## 🐾 學習

學習是一件讓人很開心、愉悅的事。當有機會能分出一段時間，定下來好好研讀技術文章或教學時，每每都讓人有能量回填的感覺，那種有一股 Input 的爽感（？。

Jerry 大在演講中除了提到較廣為人知「心流」（Flow）的觀念外，更重要的是進一步闡釋「抽象化」在學習上扮演的角色。若把學習一項技術比喻是在一個線性上，一步步的累積、疊加、前進，並且在過程中追求進入心流的狀態，以利達成所設定的目標。抽象化則是在此既有的線性上，增加了一個新的「維度」。

![](/images/functional_programming/flow.png)Flow Model by Mihaly Csikszentmihalyi

對我個人而言，另一個熟悉的相關字辭是「綜效」（Synergy）。我本身是企業管理的商科背景，所以很直覺地想到它。這個詞在管理學中的「策略管理」領域，扮演了非常重要的角色，也幾乎可以說是策略經營夢寐以求想要達到的結果之一。

正巧！到這也不難發現，當我試著把「抽象化在學習中扮演的角色」理解為「類似原本我已熟悉的綜效」時，這個過程就已經經過了抽象化。不僅達到主觀認知，又一併完成表述；可謂一兼二顧，摸蜆仔又兼洗內褲 XD。

那現在，如果確認了抽象化可以大幅增進學習的成效，並且應用在寫程式上。倘若這個天生的技能，在後天上能有更周全的培養、訓練，那該有多好呢？

Jerry 大也為此提供了他的解方。沒錯！都說到這了，我也順勢一併做前後呼應。

> Functional Programming─系統性學習抽象化的好方法。

## 🐾 最初是拳，最後是結論 🎊

這篇文不僅動筆有些晚，過程也分了幾次、耗費一些時間寫成。

主因是有一些自己不是很了解的專有名詞，像 `Functor`、`fmap`‧‧‧等。

這些在議程當中並沒有特別著墨，講者分享的主要內容我是可以理解，但程式碼舉例與專有名詞或表達的部分，倒是花了不少時間翻找資料，也是頗有收穫！

一方面自己可以學習新知，二方面寫文章分享時，也更能言之有物‧‧‧吧 XD，盡量避免因認識錯誤而導致訊息傳遞的偏誤。

個人真心認為講員講得很棒，大推 Jerry 大！

語速、節奏、幽默感，都很對味（？，內容深入淺出、鞭辟入裡，舉例精確、有趣。也因為如此，所以還特別去搜尋上一屆 Jerry 大講 RxJS 的影片 XD。

而到了今天，當我有機會坐下來重新整理思緒，嘗試綜覽全局並分享此文，我知道這個議程並不是交給我什麼武林秘笈，像是「**抽象化思考的完全指北**」，也不是教會了我「**N 大 Functional Programming 特性解析全集**」。反而是回歸更原始、更純（？）的出發點─「如何學習」與「如何思考」。

這也是為什麼，我會把 Functional Programming 設定為之後優先投入的學習主題。不妨想像一下，如果想要長久發展一座城市、一個國家，FP 就會像是其中的「基礎建設」一樣重要。而我也相信，在「基礎建設」穩健、扎實之後，未來要涉獵更廣泛或深入的主題時，才會有更多機會產生紅利加乘與綜效的結果！

![](/images/functional_programming/my_sunshine.png)Source from 老天鵝娛樂