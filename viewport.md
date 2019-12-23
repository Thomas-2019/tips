## viewport
---

### 換算絕對單位：%

你會常常需要換算絕對單位與相對單位，尤其是當你的資訊來源是設計稿時，你只能從設計稿上得知絕對的長度，此時需要改寫成相對單位。

**換算公式為：target ÷ context = result**

+ target - 原本的絕對單位
+ context - 父元素的單位
+ result - 百分比

CSS

```
.wrapper{
  width:960px;
}
.container{
  width:900px;
}
.main{
  width:650px;
}
.side{
  width:215px;
}
```

相對長度單位:px=>%

| target | ÷ | context | result |
| ------- | ------- | ------- | ------- |
| 900 px | ÷ | 960 px | 93.75% => container |
| 650 px | ÷ | 900 px | 72.222%  => main |
| 215 px | ÷ | 900 px | 23.889% => side |

如此一來就能增加網頁的彈性，但不影響到現有佈局了！

### viewport 百分比長度 (viewport percentage lengths)

這些單位會隨著 viewport 尺寸一同縮放：

+ `vw` - 對應到 width of viewport 的比例
+ `vh` - 對應到 height of viewport 的比例
+ `vmin` - 等於 `vw` 或 `vh `較小的值
+ `vmax` - 等於` vw `或 `vh `較大的值

若 viewport 的寬是 1200 像素，`1vw `會等於 viewport 寬度的 1%，也就是 12 像素。同理，`vh` 則是相對於 viewport 的高度。

### em 字體相對單位

`em` 用於文字大小，以父元素的 `font-size `為基準，例如，父元素的字體大小為 `16px`，子元素設定` 1em `等同於設定成 16 像素；若設定為` 0.5em` 則等同於 8 像素；以此類推，`2em` 會被算成 32 像素

### 限制彈性

如果你把網站全部都改寫成相對單位，內容就總是會隨著 viewport 縮放，但有時候內容不適合變得太大或太小，因此你會使用 `min-width`、`max-width`、`min-height `和 `max-height` 等屬性來控制邊界值。

例如，你有可能會這樣設定圖片尺寸：

CSS

```
img {
  width: 100%;
  max-width: 960px;
}
```
圖片在大多情況會隨著父元素縮放，但最大寬度不會超過 960px，因此可以維持圖片的清晰度。


通常我們會把網站內容整個包在 `container (或稱 wrapper) `裡，以便讓內容置中，這個 `container` 通常會設定成 `width: 100%`，但如果有人買了很大很大的螢幕，當 `container` 延展開來時，一行文字就會被拉得超長，反而造成不好的閱讀體驗。

在這種時候，你也會使用 `max-width` 來限制 `container` 的最大寬度，例如：

CSS

```
.container {
  width: 90%;
  max-width: 960px;
}
```

這樣一來，當 viewport 太大時，寬度還是可以維持。




參考資料

[相對單位](https://lighthouse.alphacamp.co/courses/17/units/2726)