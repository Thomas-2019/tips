 ## CSS 變數（Variables）
 ---

 ### CSS 變數的基本語法

```
:root {
  --main-color: #369;
}

h1 {
  color: var(--main-color);
}
```
原則：

+ 1.在`:root`命名變數，我們也可以在任意的選擇器內命名變數，後面會提到該怎麼寫，以及怎麼使用。
+ 2.`--main-color`是變數名字，`#369`是該變數的值。
+ 3.承上，變數命名的規則為：開頭必須是兩個破折號` --`。
+ 4.在要呼叫變數的選擇器裡面，使用`var()`呼叫該變數，可以把它想成 function。
+ 5.變數的大小寫是兩個不同的變數，例：`--main-color`和`--Main-Color`是不同的變數喔。

參考資料

 [SASS, LESS 退散，原生 CSS 可以使用變數啦！](https://muki.tw/tech/native-css-variables/)

 [CSS 原生變數（Variables）介紹與使用教學](https://mnya.tw/cc/word/1340.html)

 [學習CSS原生變數（CSS Variable）](https://hookey.cc/css/p/eb1013d656cbe537a7724c29c0921699.html)