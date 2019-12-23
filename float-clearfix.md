## float需搭配clearfix

***

### 解決`float`父層沒有`height`情況

#### HTML
```
<header id="head">
    <div class="container">
      <nav class="clearfix">
        <div id="logo"><a href=""><img src="https://picsum.photos/80/40/?random=1"></a>
        </div>

        <ul class="nav">
          <li><a href="">about</a></li>
          <li><a href="">content</a></li>
          <li><a href="">item</a></li>
        </ul>
      </nav>
    </div>
  </header>
  ```
  #### CSS
  
  `clearfix`是下在`float`的父層加上

  方法1:

```
.clearfix::after {
clear: both;
content: "";
display: block;
}

#logo {
  float: left;
}

.nav {
  float: right;
}
```
方法2:

```
.clearfix {
  overflow: auto;
  zoom: 1;  //IE6須加此行
}

#logo {
  float: left;
}

.nav {
  float: right;
}
```

參考資料

[關於 clear 屬性](http://zh-tw.learnlayout.com/clear.html)
