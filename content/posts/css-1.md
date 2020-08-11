---
title: "CSS 介紹 & Selector"
date: 2020-08-06T20:46:43+08:00
type: posts
tags: ["CSS"]
draft: false
---
## CSS
Cascading Style Sheets 階層式樣式表，是一種用來為結構化文件（如HTML文件或XML應用）添加樣式（字型、間距和顏色等）的語言。

## 三種加入 CSS 的方式
1. 寫在 HTML 標籤中 (inline style)
例如：
![](https://imgur.com/70G2pbh.png)  
但比較不建議，因為會跟 HTML 混在一起，不便修改及維護。
<!--more-->
2. 在 `<head>` 標籤區塊中加上 `<style>` 標籤
{{< highlight html "linenos=table, linenostart=1" >}}
<head>
  <style>
    div {
        background : red;
    }
  </style>
</head>
{{< /highlight >}}

其中 `div` 是 selector，`background: red` 則是 property 及 value。
![](https://imgur.com/D3IiYSG.png)

但仍然不建議使用此方法，因為當 html 標籤一多，style 區塊中就要有許多 selector，也是不便於修改及維護。

3. 將 CSS 獨立於單獨的檔案中，再從 HTML 中使用 `<link>` 指定 css 檔進來。
{{< highlight html "linenos=table, linenostart=1" >}}
<head>
  <link rel="stylesheet" href="./style.css" />
</head>
{{< /highlight >}}


{{< highlight css "linenos=table, linenostart=1" >}}
/* style.css */
div {
    background : grey;
}
{{< /highlight >}}

![](https://imgur.com/Sk5WoUv.png)
如此一來 HTML 及 CSS 檔案彼此獨立，可以針對單一的需求做修改而不影響另一個。

---------------------

## CSS 語法
![](https://imgur.com/0JwAeMX.png) [1]
- Selector 選擇器，用來選擇 HTML 的元素。
- { } 大括號包圍了一個宣告區域，任何寫在這個區域裡的設定，會對 HTML 中符合選擇器的元素起作用。
- Property & Value：在圖例中，我們宣告選擇器 `<h1>` 的 color 屬性的值是藍色、font-size 屬性的值是 12px。
- 多條宣告用分號 ( ; ) 隔開。

## Selector 的種類
### Universal Selector
使用 `*` ，代表選擇**所有的** html 元素。
{{< highlight css "linenos=table, linenostart=1" >}}
* {
    color : orange;
}
{{< /highlight >}}


### Element Selector
使用特定的標籤，代表選擇所有指定標籤。
{{< highlight css "linenos=table, linenostart=1" >}}
div {
    color : orange;
}
{{< /highlight >}}


### ID Selector
在一個 HTML 文件中單一 ID 只能被使用一次。選擇器以 `#` 開頭。
{{< highlight html "linenos=table, linenostart=1" >}}
<div id="a">
  test
</div>
```
```css=
#a {
  color: red;
}
{{< /highlight >}}

### Class Selector
當你有相同的東西要長得一樣時就可以把他們都命名為同一個 class。選擇器以 `.` 開頭。
{{< highlight html "linenos=table, linenostart=1" >}}
<div class="sty1">
  hello
</div>
<div class="sty1">
  world
</div>
```
```css=
.sty1 {
  color: red;
}
{{< /highlight >}}


:::info
至於何時要用 ID 、何時要用 Class，並沒有絕對的規則。但是大多的時候，Class 選擇器的使用頻率較高，因為較靈活，目的為了將幾個元素從其他元素中獨立出來做改動。但是當你要用 Javascript 的 GetElementByID 函數時，你就應該要用 ID 選擇器，因為ID 選擇器可以被 Javascript 中的 GetElementByID 函數所運用。
:::

### 同時符合
把 selector 連在一起，可以表示同時符合多種條件的選擇器。
{{< highlight html "linenos=table, linenostart=1" >}}
<div class="sty1">
  hello world
</div>
<div>
  hello html
</div>
<span class="sty1">
  hello css
</span>
<div class="sty1 bg-yellow" >
  hello js
</div>
{{< /highlight >}}


{{< highlight css "linenos=table, linenostart=1" >}}
/* 同時符合是　div 標籤以及 .sty1 class 的元素 */
div.sty1 {
  color: red;
}
/* 同時符合是　div 標籤以及 .sty1 class 以及 bg-yellow class 的元素 */
div.sty1.bg-yellow {
  color: red;
  background: yellow;
}
{{< /highlight >}}


### 選取底下的元素
{{< highlight html "linenos=table, linenostart=1" >}}
<div class="lv1">
  level 1
  <div>level 2
    <div class="bg-red">level 3</div>
  </div>
  <div class="bg-red">level 2-1</div>
</div>
{{< /highlight >}}


#### 使用 `>` 選取左邊元素的下一層右邊元素
{{< highlight css "linenos=table, linenostart=1" >}}
/*選擇 .lv1 下一層的所有的 .bg-red*/
.lv1 > .bg-red {
  color: orange;
}
{{< /highlight >}}

![](https://imgur.com/CfTiiJj.png)
#### 使用 ` ` 選取左邊元素下一層內的所有符合右邊的元素
{{< highlight css "linenos=table, linenostart=1" >}}
/*選擇 .lv1 內的所有的 .bg-red*/
.lv1 .bg-red {
  color: orange;
}
{{< /highlight >}}

![](https://imgur.com/CfTiiJj.png)

### 選取旁邊（同一層）的元素
{{< highlight html "linenos=table, linenostart=1" >}}
<div class="bg-red">div1</div>
<div>div2</div>
<div class="bg-red">div3</div>
<div class="bg-red">div4</div>
<span>123</span>
<div>456</div>
<div>789</div>
{{< /highlight >}}

#### `+` 右邊一個
{{< highlight css "linenos=table, linenostart=1" >}}
/* 選 bg-red (第三個 div) 旁邊的 bg-red (第四個 div) 標籤 */
.bg-red + .bg-red {
  background: red
}
/* 選 span 旁邊的 div */
span + div {
  background: yellow
}
{{< /highlight >}}
![](https://imgur.com/a3zm31F.png)

#### `~` 右邊全部的
{{< highlight css "linenos=table, linenostart=1" >}}
/* 選 bg-red (第一個 div) 後面所有的 bg-red 標籤 */
.bg-red ~ .bg-red {
  background: red
}
/* 選 span 後面所有的 div */
span ~ div {
  background: yellow
}
{{< /highlight >}}

![](https://imgur.com/pMntnXU.png)

這個語法很適合用在排版，通常想要將一排的物件平均均分，第一個通常要靠邊界對齊不會動，在後面每個要間格 80px 的話只需要使用 `~` 選取。
![](https://imgur.com/qHA3r2y.png)


### Pseudo-classes 偽類
#### :hover
當游標移動到指定 selector 上面時要做什麼樣的變化。
{{< highlight css "linenos=table, linenostart=1" >}}
div:hover {
  background: red;
}
{{< /highlight >}}
![](https://imgur.com/VzN9A6g.gif)

#### nth-child

{{< highlight css "linenos=table, linenostart=1" >}}
.wrapper div:first-child {  /* 選 wrapper class 下的第一個元素同時是 div */
  background: red;
}
.wrapper div:last-child {  /* 選 wrapper class 下的最後一個元素同時是 div */
  background: orange;
}
.wrapper div:nth-child(3) {   /* 選 wrapper class 下的第三個元素同時是 div */
  background: blue;
}
.wrapper div:nth-child(odd) {  /* 選 wrapper class 下的奇數位看同時是 div */
  background: yellow;
}
.wrapper div:nth-child(3n) {  /* 選 wrapper class 下的三的倍數位看同時是 div */
  background: green;
}
.wrapper div:nth-child(3n+1) {  /* 選 wrapper class 下的三的倍數加一位看同時是 div */
  background: green;
}
{{< /highlight >}}

{{< highlight html "linenos=table, linenostart=1" >}}
  <div class="wrapper">
    <div>div1</div>
    <div>div2</div>
    <div>div3</div>
    <div>div4</div>
    <div>div5</div>
    <div>div6</div>
  </div>
{{< /highlight >}}


- 其他的 Pseudo-classes
{{< highlight css "linenos=table, linenostart=1" >}}
:link /*連結平常的樣式*/
:visited /*連結查閱後的樣式*/
:active /*滑鼠按下的樣式*/
:focus /*目標為焦點的樣式*/
:lang(E) /*當語言為E的樣式*/
:first-child /*第一個元素的樣式*/
{{< /highlight >}}


更多偽類別請參考：[Pseudo-classes](https://www.w3schools.com/css/css_pseudo_classes.asp)
:::info
補充  
因為 Pseudo-classes 通常都需要使用者觸發才會有樣式的變化，會較難 debug。下面展示了如何使用開發人員工具讓我們不須使用滑鼠也能測試 Pseudo-classes。
:::
![](https://imgur.com/ZiWXe25.png)


### Pseudo-element 偽元素
可以選到某個元素的某個部分，為了與 pseudo-class 區分，以兩個冒號`::`來表示。
{{< highlight html "linenos=table, linenostart=1" >}}
<div class="wrapper">
  1000
</div>
{{< /highlight >}}

![](https://imgur.com/gr3x9Ju.png)
#### Before
{{< highlight css "linenos=table, linenostart=1" >}}
.wrapper::before {
  content: "$";
  color: red;
}
{{< /highlight >}}

![](https://imgur.com/SEB98dY.png)
#### After
{{< highlight css "linenos=table, linenostart=1" >}}
.wrapper::after {
  content: "NTD";
  color: red;
}
{{< /highlight >}}

![](https://imgur.com/xcr6JQh.png)

### 在 content 放入 selector 的 property value
{{< highlight css "linenos=table, linenostart=1" >}}
.wrapper::after {
  content: attr(class);
  color: red;
}
{{< /highlight >}}

![](https://imgur.com/2j8aZJ6.png)
{{< highlight html "linenos=table, linenostart=1" >}}
<div class="wrapper" property="value">
  1000
</div>
{{< /highlight >}}

{{< highlight css "linenos=table, linenostart=1" >}}
.wrapper::after {
  content: attr(value);
  color: red;
}
{{< /highlight >}}

![](https://imgur.com/SnnyAAs.png)

------------------------

## CSS Selector 的權重
所謂的權重就是指 css 的優先權:
- 相同權重但是後寫的 css 可以覆蓋先寫的 css
- 當兩個選擇器同時作用在一個元素，權重高的優先生效

權重大小(可以想成愈詳細的愈贏)
:::warning
!important > inline style > ID > Class/psuedo-class(偽類)/attribute（屬性選擇器） > Element
:::

### !important
!important 的權重最高，可以蓋過所有的權重，建議不要隨便使用。
{{< highlight html "linenos=table, linenostart=1" >}}
<div style="color=blue">hello</div>
{{< /highlight >}}

{{< highlight css "linenos=table, linenostart=1" >}}
div {
    color: red;!important
}
{{< /highlight >}}
最後 hello 的樣式會是採用 !important 的紅字。

一個可愛的 CSS 權重圖：
![](https://imgur.com/LtsCyMr.png)


### Reference
[1]https://www.w3schools.com/css/css_syntax.asp  
[2]https://ithelp.ithome.com.tw/questions/10183484  
[3]https://ithelp.ithome.com.tw/articles/10196454  
[4]http://www.standardista.com/css3/css-specificity/  
