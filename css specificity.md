## CSS 權重 (css specificity)

***
所謂的權重就是指 css 的優先權，例如:

  >相同權重但是後寫的 css 可以覆蓋先寫的 css
  >當兩個選擇器同時作用在一個元素，權重高的優先生效

### 先說一下基本的權重大小

#### inline style > ID > Class > Element > *

數字最左邊的權重最高，數字最右邊的權重最低

`*`
>0-0-0-0

Element
>0-0-0-1

class
>0-0-1-0

id
>0-1-0-0

inline style attribute 就是寫在 html 行內的 style
>1-0-0-0 

```
<div style="color:red">
    CSS Specificity
</div>
```

除了這些還有

psuedo-class(偽類)
>0-0-1-0

```
:nth-child() 、 :link 、 :hover 、 :focus 等
:only-of-type 、 :nth-of-type
```
attribute（屬性選擇器）
>0-0-1-0

```
[type:checkbox]、[attr]
```

那麼來試試看

`ul>li `都是 element 所以加起來是 0-0-0-2

`body div ul li a span` 總共 6 個 element 所以加起來是 0-0-0-6

`li.myclass `一個 element 加上一個 class ，所以是 0-0-1-1

`li.myclass ~ li `兩個 element 加上一個 class ，所以是 0-0-1-2

`form input[type=email]` 兩個 element 、一個 attribute，所以是 0-0-1-2



### 終極大魔王叫做`!important`
`!important` 的權重非常高，可以蓋過所有的權重
>1-0-0-0-0

```
.product{
    width: 200px !important;
}

```
只有` !important` 能超越 !important，所以沒事不要亂用

其他說明

1. `!important `是跟著每個屬性設定，所以要在屬性中：

>`color: #123456 !important;`   <== ○ 正確寫法指定覆寫
>`color: #123456 ; !important;`   <== x 錯誤寫法，覆寫不會生效

2. 類別中有多個屬性，每個屬性都要覆寫，就每個屬性值都要有` !important`

>`.classname { color:#123456; background:#987654 !important; }   `  <==  指定覆寫background，color 不受影響
 >`.classname { color:#123456 !important; background:#987654 !important; } `    <==  指定覆寫background、color

3. 除非你很清楚知道你在覆寫什麼東西，不然少用`!important`，因為他有可能導致你查錯困難。

4. CSS的權重：

>有`!important`的 element style(設定在tag中的style) >  有`!important`的css >  element style(設定在tag中的style) > css後寫的 > css先寫的

### 結論

!important > inline style > ID > Class/psuedo-class(偽類)/attribute（屬性選擇器） > Element

參考資料

[小事之 CSS 權重](https://ithelp.ithome.com.tw/articles/10196454)

[CSS 的 !important 意義](http://n.sfs.tw/content/index/10632)

[你应该知道的一些事情——CSS权重 ](https://www.w3cplus.com/css/css-specificity-things-you-should-know.html)