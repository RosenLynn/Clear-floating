# Clear-floating
CSS清除浮动的几种方法： Clear floating
## 元素怎样浮动？

1. 元素的水平方向浮动，这时候的元素只能左右移动而不能上下移动。
2. 一个浮动元素会尽量向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。
3. 浮动元素之后的元素将围绕它。
4. 浮动元素之前的元素不会受到影响。
5. 如果图像是右浮动，下面的文本流将环绕在它左边：

CSS 的 Float（浮动），会使元素向左或向右移动，其周围的元素也会重新排列。

## 浮动的应用场景   

1. 运用到图像上，float的出现最初目的是为了文字环绕效果，可以让文字环绕于图片。
2. 列表横向排列。
3. 实现两列布局 & 三列布局
## 清除浮动的方法

### 方法1： 底部插入：clear：both；

在最后一个浮动元素后面添加一个元素，为它设置clear：both；，这时候父元素就会检测子元素中最高的元素，然后以最高的元素为父元素的高度。

```html
<div class="fahter">
    <div class="big">big</div>
    <div class="small">small</div>
    <div class="clear">额外元素法</div>
</div>
```



```css
.fahter {
	width: 400px;
	border: 1px solid deeppink;
}

.big {
	width: 200px;
	height: 200px;
	background: darkorange;
	float: left;
}

.small {
	width: 120px;
	height: 120px;
	background: darkmagenta;
	float: left;
}

.footer {
	width: 900px;
	height: 100px;
	background: darkslateblue;
}

.clear {
	clear: both;
}

```



### 方法2：为父元素添加overflow: auto; 

overflow的值可以是auto或hidden，这时候就会触发BFC。

```html
<div class="fahter">
	<div class="big">big</div>
	<div class="small">small</div>
</div>
<div class="footer"></div>
```



为父元素添加overflow: auto，

```css
.fahter {
    width: 400px;
    border: 1px solid deeppink;

    overflow: hidden;   /* 触发BFC */
}

.big {
    width: 200px;
    height: 200px;
    background: darkorange;
    float: left;
}

.small {
    width: 120px;
    height: 120px;
    background: darkmagenta;
    float: left;
}
.footer {
	width: 900px;
	height: 100px;
	background: darkslateblue;
}
```



### 方法3： 伪元素

```html
<div class="fahter clearfix">
	<div class="big">big</div>
	<div class="small">small</div>
</div>
<div class="footer"></div>
```



```css
.fahter {
	width: 400px;
	border: 1px solid deeppink;
}

.clearfix:after{
	content:"";/*设置内容为空*/
	height:0;/*高度为0*/
    line-height:0;/*行高为0*/
	display:block;/*将文本转为块级元素*/
	visibility:hidden;/*将元素隐藏visibility:hidden;的作用是允许浏览器渲染它，但是不显示出来，这样才能实现清楚浮动。*/
	clear:both;/*清除浮动*/
}
.clearfix{
	*zoom:1;/*为了兼容IE ,ie6清除浮动的方式 *号只有IE6-IE7执行*/
}
.big {
	width: 200px;
	height: 200px;
	background: darkorange;
	float: left;
}

.small {
	width: 120px;
	height: 120px;
	background: darkmagenta;
	float: left;
}

.footer {
	width: 900px;
	height: 100px;
	background: darkslateblue;
}
```



### 方法4： 双伪元素

```css
.clearfix:before,.clearfix:after {
     content: "";
     display: block;
     clear: both;
}
.clearfix {
     *zoom: 1;
 }
```

