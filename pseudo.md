# simple selectors

***

type selector `h1, p, div`
universal selector `*`
attribute selector `img[alt]`
class selector `.class`
ID selector `#id`
pseudo-class `:`
pseudo-element `::`


## pseudo-classes (偽類別)

***

 `:first-child`：第一個子元素
`:last-child`：最後一個子元素
`:nth-child(數字)`：第幾個子元素 ( 注意這裡是 1 起頭，不是 0 )
`:nth-child(2n)`：挑出偶數的元素(2的倍數)( 應該說是把 2 的倍數挑出來 )
`:nth-child(2n+1)`：挑出奇數的元素(把奇數的挑出來，其他就依此類推)
`:nth-last-child(數字)`：從後面數來第幾個子元素
`:only-child`：只有一個子元素


許多元素混雜而成的，你就會發現 :first-child 無法精準地控制第一個子元素了，例如：

### HTML

```
<div id="test">
    <div>1</div>
    <span>2</span>
    <span>3</span>
    <span>4</span>
    <div>5</div>
    <span>6</span>
    <div>7</div>
</div>
```

### CSS

```
#test div, #test span{
    width:20px;
    height:20px;
    background:#ccc;
    display:inline-block;
    margin:5px;
}
```
這時候如果我們寫了

### CSS
```
#test span:first-child{
    background:#c00;
}
```

就會發現完全沒有反應！？為什麼呢？因為 child 是只所有的子元素，裏頭的 :first-child 表示 div，但又因為我們指向 span，所以導致這個 CSS 是不會被套用進去的，這也是在使用 child 的偽類很容易遇到的錯誤，卻又不知道錯誤是如何發生，那麼到這邊，或許你會問，如果交錯混雜，我又想要選取固定元素該怎麼辦呢？這時候我們就要用上 of-type 的偽類,of-type 的偽類也有以下幾種：

   `:first-of-type`：同一種元素的第一個
    `:last-of-type`：同一種元素的最後一個
    `:nth-of-type()`：同一種元素裏頭的第幾個
    `:nth-last-of-type()`：同一種元素從後面屬過來第幾個
    `:only-of-type`：只有這種元素

經過剛剛的 child 介紹，相信大家對於上述的這些名詞解釋應該都可以想像出畫面了吧，也因此如果我們要控制剛剛那串程式碼的第一個 span，我們就要這樣寫：

### CSS
```
#test span:first-of-type{
    background:#c00;
}
```

參考資料
[CSS 偽類 child 和 of-type](https://www.oxxostudio.tw/articles/201405/css-selector.html)

***


## pseudo-element (偽元素)

***

### 認識 ::before 與 ::after

`::before`、`::after` 大概是最常使用的偽元素，兩者都是以`display:inline-block`的屬性存在，`::before` 是在原本的元素「之前」加入內容，`::after` 則是在原本的元素「之後」加入內容，同時偽元素也會「繼承」原本元素的屬性，如果原本文字是黑色，偽元素的文字也會是黑色。

`::first-line` - 選取第一行。
`::first-letter` - 選取第一個字。
`::before` - 從選取元素的前面插入東西。
`::after` - 從選取元素的後面插入東西。
`::selection` - 選取文字反白後。

參考資料

[CSS 偽元素](https://www.oxxostudio.tw/articles/201706/pseudo-element-1.html)