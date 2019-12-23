## em
---

`.container` 的 `padding: 1em` 會根據本身的 `font-size: 20px` 去做計算。但如果本身沒有設定，就會往上找，依照瀏覽器預設的(約) `16px` 做計算。你可以試試看拿掉 `.container` 的 `font-size `+ 設定 body 的 `font-size: 30px`，`.container` 的` padding 1em `就會變成 `30px `～


+ `<p>` 的` line-height `是 24px，也就是：20px * 0.8 em * 1.5em
__瀏覽器預設font-size*當前字形font-size*line-height__

+ `<p> `的 `margin-bottom` 是 32px，也就是：20px * 0.8em * 2em
__瀏覽器預設font-size*當前字形font-size*margin-bottom__

參考資料

[Building Resizeable Components with Relative CSS Units](https://css-tricks.com/building-resizeable-components-relative-css-units/)