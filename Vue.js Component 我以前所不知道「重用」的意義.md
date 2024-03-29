# Vue.js Component 我以前所不知道「重用」的意義
### 可以重用的我們就一起來重用吧！

![](/images/vuejs_component_reuse/popsicle_girl.jfif)

Photo by [Brooke Cagle](https://unsplash.com/@brookecagle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

### **最初是拳 👊**

這是我的第一篇 Medium 首發文章 🎉 ，主要是因為公司老大以每篇價值 10 元的紅利鼓勵我寫分享文章，讓我在暑假時間能有摳摳買冰棒吃（所以 Cover 放冰棒圖 🤣），真的好棒棒！（咦，聽說沒寫會被抓去作人形蜈蚣啊啊啊？ OrzOrzOrz…）

### **以前我認識得 Component 重用（Reuse）**

Q: Vue.js Framework 的最大特色是什麼？

A: MVVM 與 Component 管理。

將你的網頁，依照不同的功能或區塊拆解成不同的 Component，顯而易見的好處是，當下次你有同樣或類似需求時，可以直接使用已建立好的 Component。

以前我的認識很膚淺，假若我創建了一個 Timer （計時器 / 時鐘）的 Component，當我專案中的另一頁也同樣需要這個元件時，我就可以直接引入此元件。但 GG 的是，我的認識僅止於此…

### **My Timer Component v1 ⏲️**

我的目標是藉由 Call API 的方式取得我所需的時間，假設是某個伺服器的線上時間。

首先在 `created()` 生命週期階段呼叫 `getServerTime()` 並把取得之時間用 `setInterval()` 依秒數累加，最終在 `computed()` 用 moment 套件作 format。

```
<template>
  <span>{{ timer }}</span>
</template>
```

```
<script>
  data () {
    return {
      now: '',
    }
  },

  created () {
    this.getServerTime ();
  },

  computed: {
    timer () {
      return moment (this.now).format ('YYYY/MM/DD HH:mm:ss');
    }
  },

  methods: {
    getServerTime () {
      let $vmc = this;
      Axios.get ([API])
        .then (resp => {
          $vmc.now = resp;
          setInterval (() => $vmc.now += 1000, 1000);
        })
    }
  }
</script>
```

### **My Timer Component v2 ⏲️**

老大：欸！剛剛你不是寫了一個 Timer 嗎，我這邊要用到，拿來看砍！

我：在... 在這裡... 😳

![](/images/vuejs_component_reuse/let_me_see_see.jfif)

假如現在的需求是，我們要在 **另一處 / 另一專案** 引入相同一個 Timer Component，但這次我不要顯示 Server 的時間，而是本地端的時間呢？

看來老大會很奔潰，之前 Component 的資料被綁死了，如果需要重用的話似乎就必須改寫，而且會面目全非…

```
<template>
  <span>{{ timer }}</span>
</template>
```

```
<script>
  data () {
    return {
      now: Date.now (),
    }
  },

  created () {
    this.runTimer ();
  },

  computed: {
    timer () {
      return moment (this.now).format ('YYYY/MM/DD HH:mm:ss');
  },

  methods: {
    runTimer () {
      let $vmc = this;
      setInterval (() => $vmc.current = Date.now (), 1000);
    }
  }
</script>
```

### **My Timer Component v3 ⏲️**

老大：乾！你剛剛那個 Timer 的元件超爛的… 你回去修一下再拿來借我。

我：可是… 我不知道怎麼修欸… Q_Q

老大：你可以往如何實踐 **高內聚**、**低耦合** 的特性思考，也就是說這個 Component 要考慮，能放到不同位置且適應不同需求，進而得以實踐完整功能。

基於以上的考量，我打算：

1. 把 AJAX 取得資料的部分拉到 **外層。**
2. 當 Timer 在不同的系統 / 專案套用時，把從外層取得的資料用 **props** 的方式傳遞至 Timer 子元件。
3. 為維持 Component 獨立運作，需考慮在沒有 **props** 的情況下顯示瀏覽器時間。

```
<!-- 父層元件 -->
<timer :startTime="systemTime"></timer>
```

```
<!-- Timer Component -->
<template>
  <span>{{ timer }}</span>
</template>
```

```
<script>
  props: {
    startTime: {
      type: String,
      default: '',
    },
  },

  data () {
    return {
      now: Date.now (),
      bias: 0,
    }
  },

  created () {
    this.runTimer ();
  },

  computed: {
    timer () {
      return moment (this.now + this.bias).format ('YYYY/MM/DD HH:mm:ss');
    },
  },

  methods: {
    runTimer () {
      let $vmc = this;
      setInterval (() => $vmc.now = Date.now (), 1000);
    }
  },

  watch: {
    startTime () {
      if (this.start !== '')
        this.bias = moment (this.startTime).valueOf () - this.now;
      else this.bias = 0;
    }
  }
</script>
```

備註：Bias 表示系統時間與 Local Time 的差異，也就是用 AJAX 得到的系統時間與本地瀏覽器時間的差異。

### **高內聚、低耦合、更萬用 💪**

現在這個 Timer 已經被獨立出來了，當下次有需要拿出來使用時，就可以直說...

我：老大，這我修好了，你就拿去用吧！他是一個精確、好用的 Timer（？

我：哦，對了！如果你需要他 Sync 某個時間，你就傳個 props 給他就可以了 😎。

### **最初是拳；最後是結論 😈**

好了老大，話說... 我的 10 元冰棒呢！（伸手 🤲

![](/images/vuejs_component_reuse/girl_back.jfif)


Photo by [Verne Ho](https://unsplash.com/@verneho?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)