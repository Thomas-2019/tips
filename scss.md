## SCSS

---

- scss 寫法:

```
.top-item {
  grid-column: 3/7;
  grid-row: 1/2;
  text-align: center;
    .subtitle {
      padding: 4px 8px;
      background-color: #000000;
      color: #ffffff;
      display: inline-block;
      // @extend %outline;
    }
    .title {
      font-size: 72px;
      font-weight: 900;
      // @extend %outline;
    }
}
```

+ 父選擇器，重複編寫：如要擴充頁面樣式，就會不斷的加上 .nav li .. 等父級 class 名稱，比較費工！
+ 屬性樣式，重複編寫：常會看到許多 CSS 屬性，是許多區塊都需要用到，在 SASS 沒出來前，每個區塊都需特別寫一遍，現在直接引用即可。
+ 後續維護：若哪天需要把 .nav 這個 class 名稱更換，就需全部替換，比較麻煩。
+ 漏寫問題：SASS / SCSS 有條理的節省了許多代碼編寫，降低漏寫的 Bug。

### 1.引用父選擇器 `&`

如果想在嵌套狀態下，取得外層的父選擇器，那可以使用` ＆ `，它會直接抓父選擇器給你用。

常會把它用在，如 CSS 元件狀態： `:hover`、`:focus`、`:hover`、`:link`、`:visited `等 ..，或是` :before`、`:after `，這邊上個代碼，如下：


```
/** 編譯前( sass語法 ) **/
.item-title {
    font-size: 48px;
    color: #000;
    font-weight: 900;
    text-transform: uppercase;
    position: relative; /*定義位置*/
    top: -15px;
    z-index: 11;
    &:after,
    &:before {
      content: attr(data-title);
      @extend %outline;
      position: absolute; /*left:0*/
      left: 0;
      overflow: hidden; /*將height隱藏*/
    }

/** 編譯後（ 轉為 CSS 語法輸出 ） **/
.item .item-title:after, .item .item-title:before {
  content: attr(data-title);
  position: absolute;
  /*left:0*/
  left: 0;
  overflow: hidden;
  /*將height隱藏*/
}

.item .item-title:before {
  top: -14px;
  opacity: 0.3;
  height: 20px;
  /*遮蔽的高度*/
}

.item .item-title:after {
  top: -22px;
  opacity: 0.1;
  height: 15px;
  /*遮蔽的高度*/
}
```
還有另一種用法，也常常看到，如下：

```
    /** 編譯前( sass語法 ) **/
    #main{
        &.color-2{
            background: red;
            &:before{
                border: 1px solid #ccc;
            }
        }
        &.color-3{
            background: yellow;
            &:before{
                border: 1px solid blue;
            }
        }
    }
    /** 編譯後（ 轉為 CSS 語法輸出 ） **/
    #main.color-2 {
        background: red; 
    }
    #main.color-2:before {
        border: 1px solid #ccc; 
    }
    #main.color-3 {
        background: yellow; 
    }
    #main.color-3:before {
        border: 1px solid blue; 
    }
```

### 2.變量 `$`

SASS 中使用 `$` 進行變量聲明，支持 7 種主要數據類型：

  + 數字（如：1, 1.5, 20px）
  +  字符串，帶引號和不帶引號（如："foo", 'foo', foo）
 +   顏色（如：red, #28b0b4, rgba(0, 0, 0, 0.5)）
 +   布爾值（如： true, false）
 +   空值（如： null）
 +   值列表（list），用空格或逗號分開（如：2em 1em 0 1em、 Helvetica, Arial）
  +  maps：從一個值映射到另一個（如：(key1: value1, key2: value2)）

```
/** 編譯前( sass 語法 ) **/
// 變數
$grid-column: 120px;
$grid-row: 100px;

.wrap {
  width: 960px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(8, $grid-column);
  grid-template-rows: repeat(12, $grid-row);
}
/** 編譯後（ 轉為 CSS 語法輸出 ） **/

.wrap {
  width: 960px;
  margin: 0 auto;
  display: -ms-grid;
  display: grid;
  grid-template-columns: repeat(8, 120px);
  grid-template-rows: repeat(12, 100px);
}


```

### 3.引入 `@import`

SASS 擴展了 CSS 的 `@import` 功能，允許在文件內導入其他的 SASS 或 SCSS 子文件。

 scss檔:`_reset.scss `

```
    /** 編譯前( sass 語法 ) **/
    html, body, ul, ol, a {
        margin:  0;
        padding: 0;
    }
```

 scss檔:`main.scss` 

```
/** 編譯前( sass 語法 ) **/
    @import 'reset';  <-----插入此行
    body {
        background: #a08106;
        font-size: 16px;
    }
  /** 編譯後（ 轉為 CSS 語法輸出 ） **/
    html, body, ul, ol, a {
        margin:  0;
        padding: 0;
    }
    body {
        background: #a08106;
        font-size: 16px;
    }
  ```
+ 小提醒：若有多個文件需匯入，可同時使用多個 @import 引用文件


+  把多個 scss 文件，使用 `@import `添加到  bootstrap.scss 中。之後只需監聽 --watch bootstrap.scss 這一支文件即可，假如內部 `@import` 的文件有變更，都會在 bootstrap.css 自動更新。
+  bootstrap.scss 文件內的` @import `檔案，不需要加下劃線。
+  開頭有**下劃線**的文件，在執行 sass 指令時，**不會生成新的 css 文件**，系統會自動忽略。
+  @import scss 片段文件，不用加上**副檔名**也可以，系統會自動尋找同名的副檔名 .scss 或 .sass 文件，並依序導入。


### 比較一般 CSS @import 功能

+  如果文件的副檔名是 .css ：@import "foo.css";
+  文件名以 http:// 開始 ：@import "http://foo.com/bar";
+  文件名是 url() ：@import url(foo);
+  @import 中包含媒體查詢（media queries）

### 4.混合 `@mixin` 

若是有重複的代碼，會不斷使用到，就可用混合指令（Mixin Directives），直接把樣式封裝成一個類名稱，就可以重複調用，如下：

```
    /** 編譯前( sass 語法 ) **/
    /** 定義 mixin 指令 **/
    @mixin font-main {
        font: {
          family: Arial;
          size: 16px;
          weight: 100;
        }
        color: #000;
    }
    /** 引用 mixin **/
    .box p {
        @include font-main;
    }

        /** 編譯後（ 轉為 CSS 語法輸出 ） **/
    .box p {
      font-family: Arial;
      font-size: 16px;
      font-weight: 100;
      color: #000; 
    }
  ```

+  使用 `@mixin` 定義一個「 混合 」
+  使用 `@include` 引用一個「 混合 」
+  可同時引用多個「 混合 」


**使用參數功能**

使用「 混合 」功能，有設置參數功能（ 可設定默認值 ），讓整體功能變更彈性，有點像函數的傳入參數，如下：

```
    /** 編譯前( sass語法 ) **/
    /** 定義 mixin 指令 **/
    @mixin border-set($color, $width, $style: solid) {
        border: {
            color: $color;
            width: $width;
            style: $style;
        }
    }
    @mixin background-set($color, $image, $repeat) {
        background: {
            color: $color;
            image: url($image);
            repeat: $repeat;
        }
    }
    /** 引用 mixin **/
    .box div {
        @include border-set(red, 2px);
        @include background-set(green, "../img_tree.png", 'no-repeat');
        letter-spacing: 0.5em;
    }
    /** 編譯後（ 轉為 CSS 語法輸出 ） **/
    .box div {
      border-color: red;
      border-width: 2px;
      border-style: solid;
      background-color: green;
      background-image: url("../img_tree.png");
      background-repeat: "no-repeat";
      letter-spacing: 0.5em; 
    }
```

### 5.繼承 `@extend`

「 繼承 」`@extend` 是一個滿實用的功能，若想讓多個 class 使用相同樣式，就可使用  @extend 直接繼承過來，減少重複編寫的時間，如下：

```
/** 編譯前( sass語法 ) **/
// @extend
%outline {
  outline: 1px solid red;
}

.title {
    font-size: 72px;
    font-weight: 900;
     @extend %outline;
  }

/** 編譯後（ 轉為 CSS 語法輸出 ） **/

.title {
  font-size: 72px;
  font-weight: 900;
  outline: 1px solid red;
}
```



+ 使用站位選擇器 `%` ，定義一個樣式，被定義的類，它將不會被編譯出來。
+ 若沒有標註` % `的類，也可以使用 `@extend` 引入，但定義的類會被編譯出來。
+ 有使用 `@extend` 的類，會被系統編譯整合，使用共用樣式。


**多重擴展，可引入多個選擇器**

同一個選擇器，可以使用 @extend擴展多個選擇器，這代表它繼承了擴展選擇器的樣式，如下：

```
    /** 編譯前( sass語法 ) **/
    .error {
        background-color: #fa945c;
    }
    .notice {
        font-size: 16px;
        font-family: sans-serif;
        font-color: #000;
    }
    .seriousError {
        @extend .error;
        @extend .notice;
        background-color: #ff1b1b;
    }
        /** 編譯後（ 轉為 CSS 語法輸出 ） **/
    .error, .seriousError {
      background-color: #fa945c; 
    }
    .notice, .seriousError {
      font-size: 16px;
      font-family: sans-serif;
      font-color: #000; 
    }
    .seriousError {
      background-color: #ff1b1b; 
    }
```    

### 6.操作符

SassScript 支持對數字的運算，如：（加法 +、減法 +、乘法 *、除法 /、取模 % 等 ..），來看一下代碼，如下：

```
    /** 編譯前( sass 語法 ) **/
    div a {
        $width: 500px;
        width: $width/2;             // 使用變量，和 / 
        font: 16px/10px;             // 原生CSS，不作為除法
        height: (250px/2);           // 使用了(), 和 /
        margin-left: 10px + 8px/2px; // 使用了 +, 和 /
    }
        /** 編譯後（ 轉為 CSS 語法輸出 ） **/
    div a {
      width: 250px;
      font: 16px/10px;
      height: 125px;
      margin-left: 14px; 
    }
```

簡單來說，就是增加了運算功能，有需要也可進行使用。

這邊也有另一個範例，如下：

```
    /** 編譯前( sass語法 ) **/
    .container { width: 100%; }
    article[role="main"] {
      float: left;
      width: 700px / 960px * 100%;
    }
    aside[role="complementary"] {
      float: right;
      width: 400px / 960px * 100%;
    }
        /** 編譯後（ 轉為 CSS 語法輸出 ） **/
    .container {
      width: 100%; 
    }
    article[role="main"] {
      float: left;
      width: 72.9166666667%; 
    }
    aside[role="complementary"] {
      float: right;
      width: 41.6666666667%; 
    }
```


參考資料

  [SASS教學 ＋SCSS：CSS 再進化，掌握語法攻略！](https://frankknow.com/sass-tutorial/)

  [從 CSS 到 SASS (SCSS) 超入門觀念引導](https://dotblogs.com.tw/leo_codespace/2018/06/25/174235)
