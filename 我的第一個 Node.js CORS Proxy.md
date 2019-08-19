# 我的第一個 Node.js CORS Proxy
### 我也好想有自己的 Proxy Server 啊啊啊…

![](/images/cors-proxy-server/agent-man.jpg)

Photo by [Dragos Gontariu](https://unsplash.com/@dragos126?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

### 最初是拳 👊
相信大家都知道，Call API 有時會遇到的 CORS (Cross-Origin Resource Sharing) 跨域存取問題。以前還是初學小菜雞的時候（雖然現在還是 😂），這總是讓我很困擾...

![](/images/cors-proxy-server/console-log-error.png)

Console.log 印出的 CORS 錯誤訊息

之所以說困擾，主要我最在意的是以下兩種狀況：
1. 看到很想摳（？）的 API 但摳不了
2. 看到又有人 po 面試文，面試題目中須解決跨域存取問題
今天就回顧一下之前我所學的經驗，一次解決上述我心中的傷痛 Q_Q

### CORS 與 Proxy

首先必須了解到，跨域存取的限制是來自於 **瀏覽器** ，不是源於 **API 環境** ；由此為了解決問題，我們可以考慮兩個面向：
1. 斷開（x）瀏覽器對 CORS 的限制。
2. 創造一個非瀏覽器環境，並使之對應於 API。
針對第二點說明，簡單梳理一下：

遇到問題： **Browser ↔ API** 因為 CORS 無法存取。

解決方案：以 **Browser ↔ Proxy Server ↔ API** 的模式繞過 CORS 阻隔進而實踐存取。

解決方案的關鍵核心在於，Browser 和 Proxy Server 在同網域；且 Proxy Server 與 API 互動不是藉由瀏覽器，而是用後端程式，因此最後避開了 CORS 問題。

### 動手實作啦！

今日取材

1. API: https://shibe.online
2. CORS Proxy GitHub: https://github.com/ccoenraets/cors-proxy

API & GitHub 套件，連結中都有介紹如何使用。我要用 Browser（前端） Call 我自己用 Node.js 架起來的代理伺服器（Proxy Server），然後 Proxy Server 會將請求轉發至實際的 API Server。

在 `cors-proxy` 安裝並依照指令鍵入 `node server` ，代理伺服器會被啟動在 `http://localhost:3000` 的位置。

![](/images/cors-proxy-server/proxy-server-port.png)

隨後我簡單的起了一個專案，並在 JavaScript 寫入 Request 請求。

重點部分是下圖第 1、第 4 行。依據套件需求，我在第 4 行 `xhr.setRequestHeader` 設定 `Header` 與 `API Server` 。並承先前所述，將欲請求之 API 路徑改為 `http://localhost:3000/[API]` ，如第 1 行所示。

```
let data = 'http://localhost:3000/shibes';
let xhr = new XMLHttpRequest ();
xhr.open ('get', data, true);
xhr.setRequestHeader ('Target-URL', 'http://shibe.online/api');
xhr.send ();
xhr.onload = () => {
  let json = JSON.parse (xhr.responseText);
  console.log (json);

  let image = document.querySelector ('img');
  image.src = json[0];
}
```

就當我以為要順利完成我的第一個 CORS Proxy demo 的時候，畫面並沒有順利呈現，並跳出了以下錯誤訊息。

![](/images/cors-proxy-server/console-log-error-2.png)

老實說第一時間我是不知從何著手，有點傻了 😆。

這也是這次讓我學到的寶貴經驗！這時候可以去 GitHub Repo 裡的 `Issues` 和 `Pull requests` 裡看看，其他人的經驗或想法有沒有什麼可以參考的。

![](/images/cors-proxy-server/repo-issues.png)

這個套件的最大問題之一，顯然是作者已經長時間沒有維護了。但稍微看一下不難發現這次遇到的問題，Code 該從何著手改起。

將 `Header` 的設定做出修正；把以下 Gist 原本第 5、第 12 行的 Code 改成第 6、第 13 行，主要是把內容改為 `Target-Endpoint` 的部分。

```
if (req.method === 'OPTIONS') {
  // CORS Preflight
  res.send();
} else {
  // var targetURL = req.header('Target-URL');
  var targetURL = req.header('Target-Endpoint');

  if (!targetURL) {
    res.send(500, { error: 'There is no Target-Endpoint header in the request' });
    return;
  }
  // request({ url: targetURL + req.url, method: req.method, json: req.body, headers: {'Authorization': req.header('Authorization')} },
  request({ url: targetURL + req.url, method: req.method, json: req.body, headers: { 'Authorization': req.header('Target-Endpoint') } },

    function (error, response, body) {
      if (error) {
        console.error('error: ' + response.statusCode)
      }
      //                console.log(body);
    }).pipe(res);
}
```

### 柴柴華麗登場 🎉

修正後重新啟動 Proxy Server ，畫面即可正確顯示囉！

![](/images/cors-proxy-server/success-layout.png)

### 最初是拳，最後是結論 🐾

關於 CORS / Proxy

1. 跨域存取的限制來自於 **瀏覽器（Browser）** 不是 **API 環境** 。
2. 本文討論的解決方案是以 **Browser ↔ Proxy Server ↔ API** 的模式繞過 CORS 阻隔進而實踐存取。

關於套件錯誤

1. 除了上網 Google 錯誤訊息之外，可以去 Repo 的 `Issues` 與 `Pull requests` 查看，是否有解決方案或可參考的資訊。

今天的分享也差不多要到一個段落了。以往聽到別人的面試經驗，要臨時架出一個 Proxy Server 感覺會很有時間壓力、很麻煩。但經過這次的學習，若能找到自己慣用的工具，或是修改成屬於自己的套件，在開發的效率上是很有幫助的。

另外就是在這次開發過程中，當發現有些問題是發生在套件上的時候，一時間會有點進入 **冒名頂替症候群（Impostor Syndrome）** 、有些不知所措。但經過我們家老大的指示，並且學到去 Repo 的 `Issues` 與 `Pull requests` 找解方，累積到實務的經驗確實非常寶貴！在此跟大家分享 😄。

![](/images/cors-proxy-server/shiba-inu.jpg)

Photo by [Liudmila Luchkina](https://unsplash.com/@luchkina?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)
