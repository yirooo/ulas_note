---
title: "CSS background"
date: 2020-08-06T20:46:43+08:00
type: posts
tags: ["CSS"]
draft: false
---
## background
### 背景顏色  

{{< highlight html "linenos=table,linenostart=1" >}}
<!--html-->
<div id="box1">box1</div>
<div id="box2">box2</div>
<div id="box3">box3</div>
<div id="box4">box4</div>
{{< / highlight >}}

<!--more-->

{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: yellow;
}
#box2 {
  background: #2ab4b4;
}
#box3 {
  background: rgb(117, 107, 255);
}
#box4 {
  background: rgba(117, 107, 255, 0.3); /* a 試紙透明度，值從 0 到 1*/
}
{{< / highlight >}}

![](https://imgur.com/JqH1PAs.png)


### 背景圖片
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg")
}
{{< / highlight >}}

![](https://imgur.com/JJeq55s.png)

#### height & width
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg");
  height: 500px;
  width: 2000px;
}
{{< / highlight >}}

![](https://imgur.com/xn9dIDt.png)

#### no repeat
加上 no repeat 後，指定長寬超出圖片大小也只會顯示一張圖片。
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg") no-repeat;
  height: 500px;
  width: 2000px; 
}
{{< / highlight >}}

![](https://imgur.com/sEPpMjb.png)

#### center center / top center / bottom center
- center center 指定圖片置中。
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg") no-repeat center center;
  height: 500px;
}
{{< / highlight >}}

![](https://imgur.com/vggM3P1.png)

- top center 指定圖片靠上置中對齊
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg") no-repeat top center;
  height: 500px;
}
{{< / highlight >}}

![](https://imgur.com/HrZij8s.png)

- bottom center 指定圖片靠下置中對齊
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg") no-repeat bottom center;
  height: 500px;
}
{{< / highlight >}}

![](https://imgur.com/fWHk3u4.png)

#### background-size
- 用 pixel 表示
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg") no-repeat center center;
  background-size: 300px 100px
  height: 500px;
}
#box2 {
  background: #2ab4b4;
}
{{< / highlight >}}


![](https://imgur.com/trKw6UL.png)

- 用百分比表示

{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg") no-repeat center center;
  background-size: 50% 80%
  height: 500px;
}
#box2 {
  background: #2ab4b4;
}
{{< / highlight >}}

![](https://imgur.com/UH2ANRV.png)

- contain  
會把整張圖片放進去，按照圖片長寬按照寬或高貼合。contain 主要用於背景圖大於所在內容，但卻需要將背景圖完整呈現，此時就可採用 contain 的方式，使背景圖縮小至內容的大小。
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: url("./lemon.jpg") no-repeat center center;
  background-size: contain;
  height: 200px;
}
#box2 {
  background: #2ab4b4;
}
{{< / highlight >}}

![](https://imgur.com/NXi5EEu.png)

- cover  
cover 主要用於背景圖小於所在的內容，而背景圖又不適合使用 repeat，此時就可以採用 cover 的方式，使背景圖放大至內容的大小，但此方法容易使背景圖因放大而失真。

## border
{{< highlight html "linenos=table,linenostart=1" >}}
<!--html-->
<div id="box1">box1</div>
{{< / highlight >}}

### 背景顏色
{{< highlight css "linenos=table,linenostart=1" >}}
/* style.css */
#box1 {
  background: yellow;
  border: 20px solid green;
}
{{< / highlight >}}

![](https://imgur.com/bLCPxo1.png)