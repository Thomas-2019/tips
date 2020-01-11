## Vue

### 呈現文字的方式

簡單來說有下列幾種

1. 直接輸出：{ {message}}

- 綁定在 HTML Tag 標籤上

2. 純文字: v-text
3. HTML: v-html

```
**HTML**

<div id="app">
    <section>
      <div class="container">
        <div class="title">
          <h1>{{title}}</h1>
          <h1 v-text="title"></h1>
          <h1 v-html="title"></h1>
        </div>
      </div>
    </section>
  </div>
```

```
**main.js**

  let data = {
    title: "Vue.js!",
  };

  let vm = new Vue({
    el: "#app",
    data: data,
  });
```

參考資料

[Vue 官網](https://cn.vuejs.org/v2/guide/index.html)
[VueJS](https://kanboo.github.io/2018/07/15/VueJS/)
